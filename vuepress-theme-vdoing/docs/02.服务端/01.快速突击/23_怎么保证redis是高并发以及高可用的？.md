---
title: 23_怎么保证redis是高并发以及高可用的？
date: 2019-07-16 20:45:52
permalink: /pages/40880b/
categories:
  - 服务端
  - 快速突击
tags:
  - 
---
 

![23_redis单机的瓶颈的副本](http://anlun-oss.oss-cn-shenzhen.aliyuncs.com/alun-java-interview/23_redis%E5%8D%95%E6%9C%BA%E7%9A%84%E7%93%B6%E9%A2%88%E7%9A%84%E5%89%AF%E6%9C%AC.png)

![23_redis主从实现读写分离支撑10万+的高并发的副](http://anlun-oss.oss-cn-shenzhen.aliyuncs.com/alun-java-interview/23_redis%E4%B8%BB%E4%BB%8E%E5%AE%9E%E7%8E%B0%E8%AF%BB%E5%86%99%E5%88%86%E7%A6%BB%E6%94%AF%E6%92%9110%E4%B8%87%2B%E7%9A%84%E9%AB%98%E5%B9%B6%E5%8F%91%E7%9A%84%E5%89%AF%E6%9C%AC.png)

![23_redis replica最最基本的原理的副本](http://anlun-oss.oss-cn-shenzhen.aliyuncs.com/alun-java-interview/23_redis%20replica%E6%9C%80%E6%9C%80%E5%9F%BA%E6%9C%AC%E7%9A%84%E5%8E%9F%E7%90%86%E7%9A%84%E5%89%AF%E6%9C%AC.png)

![23_redis主从复制的原理的副本](http://anlun-oss.oss-cn-shenzhen.aliyuncs.com/alun-java-interview/23_redis%E4%B8%BB%E4%BB%8E%E5%A4%8D%E5%88%B6%E7%9A%84%E5%8E%9F%E7%90%86%E7%9A%84%E5%89%AF%E6%9C%AC.png)





![23_复制的完整的基本流程的副本](http://anlun-oss.oss-cn-shenzhen.aliyuncs.com/alun-java-interview/23_%E5%A4%8D%E5%88%B6%E7%9A%84%E5%AE%8C%E6%95%B4%E7%9A%84%E5%9F%BA%E6%9C%AC%E6%B5%81%E7%A8%8B%E7%9A%84%E5%89%AF%E6%9C%AC.png)

![23_maste run id的作用的副本](http://anlun-oss.oss-cn-shenzhen.aliyuncs.com/alun-java-interview/23_maste%20run%20id%E7%9A%84%E4%BD%9C%E7%94%A8%E7%9A%84%E5%89%AF%E6%9C%AC.png)

![23_什么是99.99%高可用性的副本](http://anlun-oss.oss-cn-shenzhen.aliyuncs.com/alun-java-interview/23_%E4%BB%80%E4%B9%88%E6%98%AF99.99%25%E9%AB%98%E5%8F%AF%E7%94%A8%E6%80%A7%E7%9A%84%E5%89%AF%E6%9C%AC.png)



![23_系统处于不可用是什么意思的副本](http://anlun-oss.oss-cn-shenzhen.aliyuncs.com/alun-java-interview/23_%E7%B3%BB%E7%BB%9F%E5%A4%84%E4%BA%8E%E4%B8%8D%E5%8F%AF%E7%94%A8%E6%98%AF%E4%BB%80%E4%B9%88%E6%84%8F%E6%80%9D%E7%9A%84%E5%89%AF%E6%9C%AC.png)



![23_redis的不可用的副本](http://anlun-oss.oss-cn-shenzhen.aliyuncs.com/alun-java-interview/23_redis%E7%9A%84%E4%B8%8D%E5%8F%AF%E7%94%A8%E7%9A%84%E5%89%AF%E6%9C%AC.png)

![23_redis基于哨兵的高可用性的副本](http://anlun-oss.oss-cn-shenzhen.aliyuncs.com/alun-java-interview/23_redis%E5%9F%BA%E4%BA%8E%E5%93%A8%E5%85%B5%E7%9A%84%E9%AB%98%E5%8F%AF%E7%94%A8%E6%80%A7%E7%9A%84%E5%89%AF%E6%9C%AC.png)





![23_集群脑裂导致的数据丢失问题的副本](http://anlun-oss.oss-cn-shenzhen.aliyuncs.com/alun-java-interview/23_%E9%9B%86%E7%BE%A4%E8%84%91%E8%A3%82%E5%AF%BC%E8%87%B4%E7%9A%84%E6%95%B0%E6%8D%AE%E4%B8%A2%E5%A4%B1%E9%97%AE%E9%A2%98%E7%9A%84%E5%89%AF%E6%9C%AC.png)



![23_脑裂导致数据丢失的问题如何降低损失的副本](http://anlun-oss.oss-cn-shenzhen.aliyuncs.com/alun-java-interview/23_%E8%84%91%E8%A3%82%E5%AF%BC%E8%87%B4%E6%95%B0%E6%8D%AE%E4%B8%A2%E5%A4%B1%E7%9A%84%E9%97%AE%E9%A2%98%E5%A6%82%E4%BD%95%E9%99%8D%E4%BD%8E%E6%8D%9F%E5%A4%B1%E7%9A%84%E5%89%AF%E6%9C%AC.png)



![23_异步复制导致的数据丢失问题的副本](http://anlun-oss.oss-cn-shenzhen.aliyuncs.com/alun-java-interview/23_%E5%BC%82%E6%AD%A5%E5%A4%8D%E5%88%B6%E5%AF%BC%E8%87%B4%E7%9A%84%E6%95%B0%E6%8D%AE%E4%B8%A2%E5%A4%B1%E9%97%AE%E9%A2%98%E7%9A%84%E5%89%AF%E6%9C%AC.png)

![23_异步复制导致数据丢失如何降低损失的副本](http://anlun-oss.oss-cn-shenzhen.aliyuncs.com/alun-java-interview/23_%E5%BC%82%E6%AD%A5%E5%A4%8D%E5%88%B6%E5%AF%BC%E8%87%B4%E6%95%B0%E6%8D%AE%E4%B8%A2%E5%A4%B1%E5%A6%82%E4%BD%95%E9%99%8D%E4%BD%8E%E6%8D%9F%E5%A4%B1%E7%9A%84%E5%89%AF%E6%9C%AC.png)



1、面试题

 

如何保证Redis的高并发和高可用？redis的主从复制原理能介绍一下么？redis的哨兵原理能介绍一下么？

 

2、面试官心里分析

 

其实问这个问题，主要是考考你，redis单机能承载多高并发？如果单机扛不住如何扩容抗更多的并发？redis会不会挂？既然redis会挂那怎么保证redis是高可用的？

 

其实针对的都是项目中你肯定要考虑的一些问题，如果你没考虑过，那确实你对生产系统中的问题思考太少。

 

3、面试题剖析

 

就是如果你用redis缓存技术的话，肯定要考虑如何用redis来加多台机器，保证redis是高并发的，还有就是如何让Redis保证自己不是挂掉以后就直接死掉了，redis高可用

 

我这里会选用我之前讲解过这一块内容，redis高并发、高可用、缓存一致性

 

redis高并发：主从架构，一主多从，一般来说，很多项目其实就足够了，单主用来写入数据，单机几万QPS，多从用来查询数据，多个从实例可以提供每秒10万的QPS。

 

redis高并发的同时，还需要容纳大量的数据：一主多从，每个实例都容纳了完整的数据，比如redis主就10G的内存量，其实你就最对只能容纳10g的数据量。如果你的缓存要容纳的数据量很大，达到了几十g，甚至几百g，或者是几t，那你就需要redis集群，而且用redis集群之后，可以提供可能每秒几十万的读写并发。

 

redis高可用：如果你做主从架构部署，其实就是加上哨兵就可以了，就可以实现，任何一个实例宕机，自动会进行主备切换。