Google File System
---


## History

在 Google 早期, 最初的设想中并没有包含要构建一个新的文件系统.


首先, Google 的目标是基于廉价的商用硬件构建一个庞大的存储网络; 因此不得不假设组件会经常发生故障, 这意味着持续的监控 (constant monitor), 错误检测 (error detection), 故障容忍 (fault tolerance) 和自动恢复 (automatic recovery) 是新文件系统的必要组成部分.

另外, 尽管 Google 早期预估系统的吞吐量需求将会超出任何个体的标准, 处理数 GB 大小的文件, 数据集将包含以 TB 记的庞大信息和数百万对象. 很自然的, 我们需要重新审定传统中对 I/O 操作和块大小 (block size) 的假定. 此外也有可扩展性方面的考虑, 这将是一个明确需要可扩展兴的文件系统. 当然在早期, 没人可以能猜测到具体需要多大的可扩展性. 不过,他们很快会得到答案.

差不多在 10 年后, Google 的绝大部分难以想象的数据存储和持续增加的应用程序都开始使用 GFS.


早期之所以决定使用单一 master, 一个主要的原因是简化整体设计. 从一开始就构建一个正确的分布式 master 被认为是比较困难的并且可能会花费较长时间. 此外单一 master 的方式可以简化很多问题. 在处理副本 (replication), 垃圾回收和许多其他的活动方面, 在一个集中的地方处理要比分布式的方式简单些. 所以最后决定在单一机器上做集中化



GFS 早期设计用于支持爬虫和索引系统, 所以追求吞吐量

<div class="alert alert-warn">
High sustained bandwidth is more important than low latency
</div>


## Architecture

*  Single GFS master and multiple GFS chunk servers accessed by multiple GFS clients

*  GFS Files are divided into fixed-size chunks(64MB)

*  Each chunk is identified by a globally unique "chunkhandle" (64bits)

*  Chunk servers store chunks on local disks as Linux file

*  For reliability each chunk is replicated on multiple chunk servers(default=3)



## Further Readings

* The Google File System

* Romain Jacotin, Lecture: The Google File System

* Case Study - GFS: Evolution on Fast-forward
