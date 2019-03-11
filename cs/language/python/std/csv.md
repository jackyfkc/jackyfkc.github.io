csv
---

CSV file Reading and Writing


The so-called CSV (Comma Separated Values) format is the most common import and export format for spreadsheets and databases.



``` python
with open('eggs.csv', 'wb') as fout:
    fout.write('\xef\xbb\xbf')
    writer = csv.writer(fout, delimiter=',')
    writer.writerow(['中国', '你好', 'Wonderful Spam'])
```


## Further Reading

* [csv Documentation](https://docs.python.org/2.7/library/csv.html)