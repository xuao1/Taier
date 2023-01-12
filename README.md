# Taier

## 1. Introduction

> A distributed dispatching system that focus on different tasks  submitted  and scheduled.
>
> It's aimed at reducing the **ETL**'s cost, making the complex dependencies between tasks clearly and reducing the labor cost about submitting, scheduling and O&M.

+ O&M: Operation & Maintenance，运营和维护
+ DAG: Directed Acyclic Graph, 有向无环图，任务可以通过上下游以有向无环图的形式组装起来

> **Taier** provide an one-stop big data platform for submitting tasks, scheduling tasks, O&M, presentation about indicators.

**Taier** 是一个开源的分布式 DAG 调度系统，专注不同任务的提交和调度。旨在降低 ETL 开发成本，解决任务之间复杂的依赖关系和提交、调度、运维带来的上手成本

在 **Taier** 上进行 ETL 开发，不用关心任务错综复杂的依赖关系与底层的大数据平台的架构实现，将工作的重心更多地聚焦在业务之中

**Taier** 提供了一个提交、调度、运维、指标信息展示的一站式大数据开发平台

![image-20230110105504813](C:\Users\86198\AppData\Roaming\Typora\typora-user-images\image-20230110105504813.png)

## 2. 使用的工具

#### Hadoop

是一个分布式系统基础架构，主要解决海量数据的存储和海量数据的分析计算问题。

Hadoop2.x 中，MapReduce 负责计算，Yarn 负责资源调度，HDFS 负责数据存储

#### YARN

YARN 是一个资源调度平台，负责为运算程序提供服务器运算资源，相当于一个分布式的操作系统平台

#### HDFS

Hadoop Distributed File System，是 Hadoop 中的存储组件，是一个分布式文件系统，以流式数据访问模式存储超大文件，将数据分块存储到一个商业硬件集群的不同机器上。

#### Flink

是一个框架和分布式处理引擎，用于在无边界和有边界数据流上进行有状态的计算。Flink 能在所有常见集群环境中运行，并能以内存速度和任意规模进行计算。

Flink 集成了所有常见的集群资源管理器，比如 Hadoop YARN

#### Chunjun

> ChunJun is a distributed integration framework, and currently is based on Apache Flink.

一款稳定、易用、高效、批流一体的数据集成框架，目前基于实时计算引擎 Flink 实现多种异构数据源之间的数据同步与计算。

Chunjun 是一个基于 Flink 的批流统一的数据同步工具，既可以采集静态的数据。 比如 MySQL，HDFS 等，也可以采集实时变化的数据，比如 MySQL binlog，Kafka 等。

Taier 使用 Chunjun 来实现数据同步、实时采集等功能。

**特性：**

+ 基于实时计算引擎 Flink，支持 JSON 模版配置任务，兼容 Flink SQL 语法；
+ 支持分布式运行，支持 flink-standalone、yarn-session、yarn-per job 等多种提交方式；
+ 支持多种异构数据源，可支持 MySQL、Oracle、SQLServer、Hive、Kudu 等20多种数据源的同步与计算；
+ 易拓展，高灵活性，新拓展的数据源插件可以与现有数据源插件即时互通，插件开发者不需要关心其他插件的代码逻辑；
+ 不仅仅支持全量同步，还支持增量同步、间隔轮训；
+ 批流一体，不仅仅支持离线同步及计算，还兼容实时场景；
+ 支持脏数据存储，并提供指标监控等；
+ 配合 checkpoint 实现断点续传；
+ 不仅仅支持同步 DML 数据，还支持 Schema 变更同步；

#### MySQL

工具书：[第3章：教程_MySQL 中文文档 (mysqlzh.com)](https://www.mysqlzh.com/doc/24.html)

`mysql -h host -u user -p`

host 和 user 分别代表 MySQL 服务器运行的主机名和 MySQL 账户用户名。输入口令，就连接上了 MySQL Server，输入 `exit` 断开连接。

一个命令通常由 SQL 语句组成，随后跟着一个分号

要想将文本文件 `“pet.txt”` 装载到 pet 表中，使用这个命令：

```mysql
mysql> LOAD DATA LOCAL INFILE '/path/pet.txt' INTO TABLE pet;
```

如果想要一次增加一个新记录，可以使用 INSERT 语句。最简单的形式是，提供每一列的值，其顺序与 CREATE TABLE 语句中列的顺序相同。假定 Diane 把一只新仓鼠命名为 Puffball，你可以使用下面的 INSERT 语句添加一条新记录：

```mysql
mysql> INSERT INTO pet
    -> VALUES ('Puffball','Diane','hamster','f','1999-03-30',NULL);
```

#### PostgreSQL

工具书：[PostgreSQL 教程 | 菜鸟教程 (runoob.com)](https://www.runoob.com/postgresql/postgresql-tutorial.html)

是一个客户/服务器关系型数据库管理系统。

## 3. 功能介绍

### 3.1 集群配置

控制台是维护底层资源的管理平台，分为：

**队列管理，资源管理，多集群管理**

多集群管理用于配置任务实力运行所依赖的底层组件，比如资源调度组件 YARN、存储组件 HDFS、计算组件 Flink 等。

### 3.2 任务类型

+ 数据同步
+ 实时采集
+ Flink SQL
+ Spark SQL
+ Hive SQL



## References

[DTStack/Taier: Taier is a big data development platform for submission, scheduling, operation and maintenance, and indicator information display (github.com)](https://github.com/DTStack/Taier)

[Taier介绍 | Taier (dtstack.github.io)](https://dtstack.github.io/Taier/docs/guides/introduction)

[快速开始 - 快速上手 - 《Taier（太阿）v1.1 使用教程》 - 书栈网 · BookStack](https://www.bookstack.cn/read/Taier-1.1-zh/46c420e8b246974c.md)

[chunjun: 基于flink的分布式数据同步框架 (gitee.com)](https://gitee.com/dtstack_dev_0/chunjun)

[第1章：一般信息_MySQL 中文文档 (mysqlzh.com)](https://www.mysqlzh.com/doc/1.html)

[PostgreSQL 教程 | 菜鸟教程 (runoob.com)](https://www.runoob.com/postgresql/postgresql-tutorial.html)
