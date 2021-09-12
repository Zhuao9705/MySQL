# InnoDB 和 ACID 模型

[ACID](https://www.docs4dev.com/docs/zh/mysql/5.7/reference/glossary.html#glos_acid)模型是一组数据库设计原则，这些原则强调了对于业务数据和关键任务应用程序很重要的可靠性方面。 MySQL 包含诸如`InnoDB`存储引擎之类的组件，这些组件与 ACID 模型紧密相关，因此数据不会损坏，结果不会因软件崩溃和硬件故障等异常情况而失真。当您依靠符合 ACID 的功能时，无需重新发明一致性检查和崩溃恢复机制。如果您有其他软件保护措施，超可靠的硬件或可以容忍少量数据丢失或不一致的应用程序，则可以调整 MySQL 设置以牺牲一些 ACID 可靠性，以获得更高的性能或吞吐量。

以下各节讨论 MySQL 功能(尤其是`InnoDB`存储引擎)如何与 ACID 模型的类别进行交互：

- **A** ：原子性。

- **C** ：一致性。
- **I：** ：隔离。
- **D** ：耐久性。

## Atomicity

**这边解释一下原子性：事务是最小的执行单位，不允许分割。事务的原子性确保动作要么全部完成，要么全部失败回滚；**

ACID 模型的“原子性”方面主要涉及`InnoDB` [transactions](https://www.docs4dev.com/docs/zh/mysql/5.7/reference/glossary.html#glos_transaction)。相关的 MySQL 功能包括：

- Autocommit setting.
- [COMMIT](https://www.docs4dev.com/docs/zh/mysql/5.7/reference/commit.html) statement.
- [ROLLBACK](https://www.docs4dev.com/docs/zh/mysql/5.7/reference/commit.html) statement.
- `INFORMATION_SCHEMA`table 中的操作数据。

## Consistency

**简单解释： 一致性是指，在每次提交或回滚之后以及正在进行事务期间，数据库始终保持一致状态。如果正在多个 table 之间更新相关数据，则查询将看到所有旧值或所有新值，而不是新旧值的混合。**

ACID 模型的“一致性”方面主要涉及内部`InnoDB`处理，以防止数据崩溃。相关的 MySQL 功能包括：

- `InnoDB` [doublewrite buffer](https://www.docs4dev.com/docs/zh/mysql/5.7/reference/glossary.html#glos_doublewrite_buffer).
- `InnoDB` [crash recovery](https://www.docs4dev.com/docs/zh/mysql/5.7/reference/glossary.html#glos_crash_recovery).

## Isolation

 **简单解释：隔离性是指，并发执行的各个事务之间不能互相干扰，即一个事务内部的操作及使用的数据，对并发的其他事务是隔离的。**

ACID 模型的“隔离”方面主要涉及`InnoDB` [transactions](https://www.docs4dev.com/docs/zh/mysql/5.7/reference/glossary.html#glos_transaction)，尤其是适用于每个事务的[isolation level](https://www.docs4dev.com/docs/zh/mysql/5.7/reference/glossary.html#glos_isolation_level)。相关的 MySQL 功能包括：

- [Autocommit](https://www.docs4dev.com/docs/zh/mysql/5.7/reference/glossary.html#glos_autocommit) setting.
- `SET ISOLATION LEVEL`声明。
- `InnoDB` [locking](https://www.docs4dev.com/docs/zh/mysql/5.7/reference/glossary.html#glos_locking)的底层详细信息。在性能调整期间，您可以通过`INFORMATION_SCHEMA`table 查看这些详细信息。

## Durability

**简单解释：持久性是指，一个事务被提交之后。它对数据库中数据的改变是持久的，即使数据库发生故障也不应该对其有任何影响。**

ACID 模型的“耐用性”方面涉及与您的特定硬件配置交互的 MySQL 软件功能。由于取决于您的 CPU，网络和存储设备的功能的可能性很多，因此为具体的准则提供最复杂的方面。 (这些准则可能采取购买“新硬件”的形式.)相关的 MySQL 功能包括：

- `InnoDB` [doublewrite buffer](https://www.docs4dev.com/docs/zh/mysql/5.7/reference/glossary.html#glos_doublewrite_buffer)，由[innodb_doublewrite](https://www.docs4dev.com/docs/zh/mysql/5.7/reference/innodb-parameters.html#sysvar_innodb_doublewrite)配置选项打开和关闭。
- 配置选项[innodb_flush_log_at_trx_commit](https://www.docs4dev.com/docs/zh/mysql/5.7/reference/innodb-parameters.html#sysvar_innodb_flush_log_at_trx_commit)。
- 配置选项[sync_binlog](https://www.docs4dev.com/docs/zh/mysql/5.7/reference/replication-options-binary-log.html#sysvar_sync_binlog)。
- 配置选项[innodb_file_per_table](https://www.docs4dev.com/docs/zh/mysql/5.7/reference/innodb-parameters.html#sysvar_innodb_file_per_table)。
- 存储设备(例如磁盘驱动器，SSD 或 RAID 阵列)中的写缓冲区。
- Batteries 后备存储设备中的缓存。
- 用于运行 MySQL 的 os，特别是它对`fsync()`系统调用的支持。
- 不间断电源(UPS)保护运行 MySQL 服务器并存储 MySQL 数据的所有计算机服务器和存储设备的电源。
- 您的备份策略，例如备份的频率和类型以及备份保留期。
- 对于分布式或托管数据应用程序，MySQL 服务器的硬件所位于的数据中心的特定特性，以及数据中心之间的网络连接。
