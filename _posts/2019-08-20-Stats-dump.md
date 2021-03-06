---
title: 一键导出 TiDB 统计信息
date: 2019-08-20 00:00:00
categories:
- TiDB 学习
tags:
- TiDB
- 统计信息
typora-root-url: ../../WalterWJ.github.io
---

# **一键导出 TiDB 统计信息**

# 目的

在使用 TiDB 的过程中，经常会遇到一些慢 SQL 的问题，当需要寻求 TIDB 原厂协助，或者在[官方论坛](https://asktug.com/)发帖的时候，大概率需要收集以下信息：

* 版本信息：`select tidb_version();`
* 表结构：`show create table table_name;`
* 表的统计信息： `curl http://tidb_ip:status_port/stats/dump/db_name/table_name > table_name.json`(默认端口为 10080)
* 执行 SQL 和执行计划

统计信息相关官方介绍: [统计信息简介](https://pingcap.com/docs-cn/v3.0/reference/performance/statistics/)

为了快速拿到相关表的统计信息，表结构，并且方便官方快速导入表结构和统计信息。因此写了相关脚本，进行一键导出导入。

**注意：** 导入统计信息的时候，需要创建对应的库，否则导入会报错。

# 脚本书写

功能：

1.  可以导出整个集群的表结构和统计信息

2.  可以指定库导出表结构和统计信息

3.  可以指定表进行导出相关表结构和统计信息

  **会生成一个压缩文件，其中 schema.sql 中是创建表/库语句，和 load 统计信息语句。**

# 用法
```shell
./Stats_dump.py -h

usage: Stats_dump.py [-h] [-tu TIDB] [-H MYSQL] [-u USER] [-p PASSWORD]

                     [-d DATABASE] [-t TABLES]

Export statistics and table structures

optional arguments:

  -h, --help   show this help message and exit

  -tu TIDB     tidb status url, default: 127.0.0.1:10080

  -H MYSQL     Database address and port, default: 127.0.0.1:4000

  -u USER      Database account, default: root

  -p PASSWORD  Database password, default: null

  -d DATABASE  Database name, for example: test,test1, default: None

  -t TABLES    Table name (database.table), for example: test.test,test.test2, default: None
```

* 参数说明
  + `-tu` 后填 TIDB 的 IP 地址和 status 端口，端口默认为 10080
  + `-H` 后填 TiDB 的 IP 地址和连接端口，端口默认是 4000
  + `-u` 为数据库登录账户
  + `-p` 为数据库登录密码
  + `-d` 为需要导出统计信息的库，如果使用该参数，就是代表将会导出对应库所有表的统计信息和表结构。比如填 `-d test1,test2`，就是讲 `test1` 和 `test2` 库下的表的统计信息和表结构导出
  + `-t` 导出对应表的统计信息、表结构。需要注意格式：`database_name.table_name`。比如填 `-t test1.t1,test2.t2`，代表将会导出 test1 库 t1 表和 test2 库 t2 表的表结构和统计信息。

* 注意
  + 如果 `-d` 和 `-t` 都没有指定，默认是导出除了系统表以外所有表的统计信息和表结构。
  + 不会导出 `"INFORMATION_SCHEMA", "PERFORMANCE_SCHEMA","mysql", "default"` 库的表结构和统计信息。
  + 该脚本在 `TiDB 3.0` 中执行没有问题，但是由于 2.1 版本不支持 `show create database if not exists db_name;` 语法，如果导出 2.1 版本的 TIDB 统计信息，需要手动修改脚本 [Stats_dump.py](https://github.com/WalterWj/PingCAP/blob/master/Stats_dump.py#L107) 107 行，将 `if not exists` 删除，即可。

[脚本链接](https://github.com/WalterWj/PingCAP/blob/master/Stats_dump.py)

