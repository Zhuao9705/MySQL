### 验证 InnoDB 是默认存储引擎

- 发出[`SHOW ENGINES`](https://dev.mysql.com/doc/refman/5.7/en/show-engines.html)语句以查看可用的 MySQL 存储引擎。`DEFAULT`在`SUPPORT` 列中寻找 。

```
SHOW ENGINES;
```

这边显示显示一下真实运行结果：

![image-20210911184215680](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210911184215680.png)

可以看到默认的是Innodb存储引擎。

- 也可以直接查询查询 [`INFORMATION_SCHEMA.ENGINES`](https://dev.mysql.com/doc/refman/5.7/en/information-schema-engines-table.html)表，例如

```
SELECT * FROM INFORMATION_SCHEMA.ENGINES;
```

![image-20210911184146544](C:\Users\Administrator\AppData\Roaming\Typora\typora-user-images\image-20210911184146544.png)