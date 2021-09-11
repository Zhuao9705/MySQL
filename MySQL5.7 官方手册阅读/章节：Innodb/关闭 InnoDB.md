### 关闭 InnoDB

Oracle 建议`InnoDB`将典型数据库应用程序作为首选存储引擎，从在本地系统上运行的单用户 wiki 和博客，到推动性能极限的高端应用程序。在 MySQL 5.7 中，`InnoDB`是新表的默认存储引擎。

> Important
>
> `InnoDB` cannot be disabled. The [`--skip-innodb`](https://dev.mysql.com/doc/refman/5.7/en/innodb-parameters.html#option_mysqld_innodb) option is deprecated and has no effect, and its use results in a warning. Expect it to be removed in a future MySQL release. This also applies to its synonyms (`--innodb=OFF`, `--disable-innodb`, and so forth).

**原文里写到Innodb是不能被禁用的。**