[Optimization](https://dev.mysql.com/doc/refman/5.7/en/optimization.html)
----


## Optimize Tables
...


## Optimize SQL statements
...


**InnoDB Queries**

Each query can only make use of one index


## Using Index

### Multi-Column Indexes

The order of columns in a multicolumn B-Tree index means that the index is sorted first by the leftmost column, then by the next column, and so on.

There is an old rule of thumb for choosing column order: place the most selective columns first in the index.

Placing the most selective columns first can be a good idea when there is no sorting or grouping to consider, and thus the purpose of the index is only to optimize `WHERE` lookups.



## Optimize the MySQL Server
...

