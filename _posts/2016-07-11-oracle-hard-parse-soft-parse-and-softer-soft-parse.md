---
layout: post
title: "Oracle: Hard Parse, Soft Parse and Softer Soft Parse"
description: ""
date: 2016-07-11
time: 13:57:44
author: Lambert Bao
header_img: img/bg-1.jpg
category: 
tags: [Oracle, database, parse, hard parse, soft parse, softer soft parse]

---

### Oracle SQL执行流程

![sql_exec_process](/img/in_post/sql_exec_process.png)

### 硬解析(Hard Parse)

* 语法、语义及权限检查；

* 查询转换（通过应用各种不同的转换技巧，会生成语义上等同的新的SQL语句，如count(1)会转为count(*)）

* 根据统计信息生成执行计划（找出成本最低的路径，这一步比较耗时）

* 将游标信息（执行计划）保存到库缓存(SGA Shared Pool)中

### 软解析(Soft Parse)

* 语法、语义及权限检查

* 将整条SQL hash后从库缓存中获取匹配的执行计划


### 更软解析（会话缓存 Softer Soft Parse）

当库缓存中的同一语句游标执行过3次解析之后，该游标会被移动到pga区的session cursor cache中，若再有相同的语句执行，则Oracle会跳过软、硬解析的所有步骤，直接从会话缓存中获取执行计划并执行。

### Oracle内存结构

关于本文中提及的Oracle相关内存结构可以参考官方文档：[Oracle Database Memory Architecture](http://docs.oracle.com/database/121/CNCPT/memory.htm#CNCPT7778)

附文档中一张简要的结构说明图：
![oracle_database_memory_structures](/img/in_post/oracle_database_memory_structures.gif)