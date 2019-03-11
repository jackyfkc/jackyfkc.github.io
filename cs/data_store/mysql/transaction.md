Transaction 事务
---

A transaction is a transformation of state which has the properties of atomicity (all or nothing), durability (effects survive failures) and consistency (a correct transformation).

The transaction concept is key to the structuring of data management applications.


## ACID 酸 :-)

### Atomic 原子性

A transaction's changes to the state are atomic: either all happen or none happen


### Consistency 一致性

A transaction is a correct transformation of the state. The actions taken as a group do not violate any of the integrity constraints associated with the state.



### [Isolation level 隔离级别](http://dev.mysql.com/doc/refman/5.5/en/innodb-transaction-isolation-levels.html)


#### Repeatable Read 可重复读

The default isolation level, in this level, InnoDB use `next-key` locking strategy to prevents phantom reads: rather than locking only the rows you've touched in a query, InnoDB locks gaps in the index structure as well, preventing phantom rows from being inserted.

InnoDB 的默认隔离级别; 在这个级别上, InnoDB 使用 `next-key` 锁策略避免了幻读: 不仅仅对查询的 rows 上锁, 同时也锁住了索引结构上间隙 gap, 用以阻止幻影行的写入. **注意这与 SQL ANSI 标准不同, 后者在这个级别会出现幻读**.


#### Read Committed 读提交
...


#### Read Uncommitted 读未提交

适合的场景极少, 极少使用


#### Serializable 序列化

...


### Durability 持久化

Once a transaction completes successfully(commits), its changes to the state survive failure


* [innodb_flush_log_at_trx_commit](https://dev.mysql.com/doc/refman/8.0/en/innodb-parameters.html#sysvar_innodb_flush_log_at_trx_commit)

    Controls the balance between strict `ACID` compliance for commit operations and higher performance that is possible when commit-related I/O operations are rearranged and done in batches. You can achieve better performance by changing the default value but then you can lose up to a second of transactions in a crash.

* innodb_flush_log_at_timeout

    Write and flush the logs every **N** seconds. `innodb_flush_log_at_timeout` allows the timeout period between flushes to be increased in order to reduce flushing and avoid impacting performance of binary log group commit.


For durability and consistency in a replication setup that uses InnoDB with transactions:

* If binary logging is enabled, set `sync_binlog=1`.

* Always set `innodb_flush_log_at_trx_commit=1`.


## Further Readings

* The Transaction Concept: Virtues and Limitations, Jim Gray

    http://jimgray.azurewebsites.net/papers/thetransactionconcept.pdf

* [Transactions on InnoDB](https://blogs.oracle.com/mysqlinnodb/)

* [MSDN - Repeatable Read isolation level](https://blogs.msdn.microsoft.com/craigfr/2007/05/09/repeatable-read-isolation-level/)
