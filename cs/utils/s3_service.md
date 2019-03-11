This class is used to uploading files to s3, supporting large file (use Multipart Upload + eventlet).


```python
import os
import logging

import greenlet
import eventlet

eventlet.patcher.monkey_patch(all=False, socket=True)

from boto import s3
from filechunkio import FileChunkIO

log = logging.getLogger(__name__)


class UploadService(object):
    """ use AWS s3 to store files
    """

    # It is recommended that to use Multipart Upload for objects greater than 100MB
    LARGE_FILE_LOW_WATER = 100 * 1024 * 1024

    # AWS asks the size of each part must be between [5 MB, 5GB]
    #  except the last one
    MIN_CHUNK_SIZE, MAX_CHUNK_SIZE = 5 * 1024 * 1024, 64 * 1014 * 1024

    # When using multi-part upload mechanism, we can choose any part number
    # between 1 and 10,000.
    MAX_PART_NUMBER = 10000

    def __init__(self, region, access_id, access_key, bucket_name):
        self._client = s3.connect_to_region(region,
                                            aws_access_key_id=access_id,
                                            aws_secret_access_key=access_key)
        # Assume that the bucket has already exist
        self._bucket = self._client.get_bucket(bucket_name, validate=False)

    @property
    def bucket(self):
        """ The bucket where we store files
        """
        return self._bucket

    def put_string(self, key_name, content):
        """ store string
        """
        key = self._bucket.new_key(key_name)
        return key.set_contents_from_string(content) == len(content)

    def put_file(self, key_name, file_name):
        source_size = os.stat(file_name).st_size
        if source_size < self.LARGE_FILE_LOW_WATER:
            self.put_small_file(key_name, file_name, source_size)
        else:
            self.put_large_file(key_name, file_name, source_size)

    def put_small_file(self, key_name, file_name, source_size):
        """ store small file using generic file IO
        """
        key = self._bucket.new_key(key_name)
        if source_size == 0:
            key.set_contents_from_string('')
            return True
        size = key.set_contents_from_filename(file_name)
        return size == source_size

    def put_large_file(self, key_name, file_name, source_size, pool_size=10):
        """ Put file to aws s3 using multi-part upload mechanism, use green thread to speed up

        Refers to
            [Official document] http://docs.aws.amazon.com/AmazonS3/latest/dev/mpuoverview.html
            [Python document] http://boto.readthedocs.org/en/latest/s3_tut.html
            [Example] http://www.topfstedt.de/

        Args:
            file_name: the name of the uploaded file
            key_name: The name of the key that will ultimately result from this upload operation
            pool_size: specify the size of the green pool

        Returns:
            True if succeed, otherwise false
        """
        if source_size >= self.MAX_CHUNK_SIZE * self.MAX_PART_NUMBER:
            raise RuntimeError('Too large file - %s' % file_name)

        mpu = self._bucket.initiate_multipart_upload(key_name)

        chunk_size = min(max(self.MIN_CHUNK_SIZE, source_size / 10), self.MAX_CHUNK_SIZE)
        num_parts = (source_size - 1) / chunk_size + 1

        pool = eventlet.GreenPool(pool_size)
        for num in xrange(num_parts):
            offset = chunk_size * num
            length = min(chunk_size, source_size - offset)
            pool.spawn_n(self._upload_part, mpu, num+1, file_name, offset, length)
        pool.waitall()

        mpu.complete_upload()
        return True

    @staticmethod
    def _upload_part(mpu, part_num, file_name, offset, length, retries_num=3):
        """ upload a part/chunk of file, used together with put_large_file()

        Args:
            mpu: an object of s3.multipart.MultiPartUpload type
            part_num: the number of this part

            file_name: the name of the uploaded file
            offset: the amount of bytes that the chunks starts after the file's first byte
            length: the amount of bytes the chunk has
        """
        try:
            with FileChunkIO(file_name, 'rb', offset=offset, bytes=length) as fp:
                mpu.upload_part_from_file(fp, part_num=part_num)
        except:
            if retries_num > 1:
                UploadService._upload_part(mpu, part_num, file_name, offset,
                                           length, retries_num-1)
            else:
                # Note that the GreenPool would swallow all exceptions except
                # GreenletExit, ...
                log.fatal('Fail to upload part - %s - %s', part_num, file_name, exc_info=1)
                raise greenlet.GreenletExit()
```
