---
title: 28_你能说说redis的并发竞争问题该如何解决吗？
date: 2019-07-15 19:49:56
permalink: /pages/ea90bb/
categories:
  - 服务端
  - 快速突击
tags:
  - 
---
 ![28_01_redis并发竞争问题以及解决方案的副本](http://anlun-oss.oss-cn-shenzhen.aliyuncs.com/alun-java-interview/28_01_redis%E5%B9%B6%E5%8F%91%E7%AB%9E%E4%BA%89%E9%97%AE%E9%A2%98%E4%BB%A5%E5%8F%8A%E8%A7%A3%E5%86%B3%E6%96%B9%E6%A1%88%E7%9A%84%E5%89%AF%E6%9C%AC.png)





1、面试题

 

redis的并发竞争问题是什么？如何解决这个问题？了解Redis事务的CAS方案吗？

 

2、面试官心里分析

 

这个也是线上非常常见的一个问题，就是多客户端同时并发写一个key，可能本来应该先到的数据后到了，导致数据版本错了。或者是多客户端同时获取一个key，修改值之后再写回去，只要顺序错了，数据就错了。

 

而且redis自己就有天然解决这个问题的CAS类的乐观锁方案

 

3、面试题剖析

