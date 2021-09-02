# **Innodb简介**

`InnoDB`是一种兼顾高可靠性和高性能的通用存储引擎。在 MySQL 5.7 中，`InnoDB`是默认的 MySQL 存储引擎（从mysql5.5.5开始）。除非配置了不同的默认存储引擎，否则发出[`CREATE TABLE`](https://dev.mysql.com/doc/refman/5.7/en/create-table.html)不带`ENGINE` 子句的语句会创建一个`InnoDB`表。



#### InnoDB 的主要优势

1. **它的 DML 操作遵循 ACID 事务模型，事务具有提交、回滚和崩溃恢复功能，以保护用户数据。**（与此相对，Myisam是不支持事务的）
2. **支持行级锁，并且和Oracle 风格的一致读取提高了多用户并发性和性能**（Myisam只支持表级锁）。
3. **`InnoDB`表将您的数据排列在磁盘上以优化基于主键的查询。每个 `InnoDB`表都有一个称为聚集索引的主键索引，用于组织数据以最小化主键查找的 I/O。**（Innodb主键索引是聚簇索引，辅助索引是非聚簇索引；而Mysiam是非聚簇索引）
4. **为维护数据完整性，`InnoDB`支持 `FOREIGN KEY`约束。使用外键，检查插入、更新和删除以确保它们不会导致相关表之间的不一致。**（Myisam是不支持外键的）



#### Innodb存储引擎特性：

![image](https://user-images.githubusercontent.com/87631434/131850009-b9789e25-a6ef-46f1-b9ba-51d5634045d9.png)
