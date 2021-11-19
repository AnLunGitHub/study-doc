---
title: 24_怎么保证redis挂掉之后再重启数据可以进行恢复？
date: 2020-04-01 10:14:28
permalink: /pages/c96e0f/
categories:
  - 服务端
  - 快速突击
tags:
  - 
---
 

![24_redis持久化的意义的副本](http://anlun-oss.oss-cn-shenzhen.aliyuncs.com/alun-java-interview/24_redis%E6%8C%81%E4%B9%85%E5%8C%96%E7%9A%84%E6%84%8F%E4%B9%89%E7%9A%84%E5%89%AF%E6%9C%AC.png)

![24_AOF rewrite原理剖析的副本](http://anlun-oss.oss-cn-shenzhen.aliyuncs.com/alun-java-interview/24_AOF%20rewrite%E5%8E%9F%E7%90%86%E5%89%96%E6%9E%90%E7%9A%84%E5%89%AF%E6%9C%AC.png)



![24_RDB和AOF的介绍的副本](http://anlun-oss.oss-cn-shenzhen.aliyuncs.com/alun-java-interview/24_RDB%E5%92%8CAOF%E7%9A%84%E4%BB%8B%E7%BB%8D%E7%9A%84%E5%89%AF%E6%9C%AC.png)

![24_RDB丢失数据的问题的副本](http://anlun-oss.oss-cn-shenzhen.aliyuncs.com/alun-java-interview/24_RDB%E4%B8%A2%E5%A4%B1%E6%95%B0%E6%8D%AE%E7%9A%84%E9%97%AE%E9%A2%98%E7%9A%84%E5%89%AF%E6%9C%AC.png)

1、面试题

 

redis的持久化有哪几种方式？不同的持久化机制都有什么优缺点？持久化机制具体底层是如何实现的？

 

2、面试官心里分析

 

redis如果仅仅只是将数据缓存在内存里面，如果redis宕机了，再重启，内存里的数据就全部都弄丢了啊。。。。。。你必须得用redis的持久化机制，将数据写入内存的同时，异步的慢慢的将数据写入磁盘文件里，进行持久化

 

如果redis宕机了，重启启动，自动从磁盘上加载之前持久化的一些数据，就可以了，也许会丢失少许数据，但是至少不会将所有数据都弄丢 

 

这个其实一样，针对的都是redis的生产环境可能遇到的一些问题，就是redis要是挂了再重启，内存里的数据不就全丢了？能不能重启的时候把数据给恢复了？

 

3、面试题剖析