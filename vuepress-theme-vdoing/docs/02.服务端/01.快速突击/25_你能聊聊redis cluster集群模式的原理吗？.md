---
title: 25_你能聊聊redis cluster集群模式的原理吗？
date: 2019-07-15 19:42:57
permalink: /pages/d25fd7/
categories:
  - 服务端
  - 快速突击
tags:
  - 
---
 ![25_redis单master架构的容量的瓶颈问题的副本](http://anlun-oss.oss-cn-shenzhen.aliyuncs.com/alun-java-interview/25_redis%E5%8D%95master%E6%9E%B6%E6%9E%84%E7%9A%84%E5%AE%B9%E9%87%8F%E7%9A%84%E7%93%B6%E9%A2%88%E9%97%AE%E9%A2%98%E7%9A%84%E5%89%AF%E6%9C%AC.png)





![25_redis如何通过master横向扩容支撑1T+数据量的副本.png](http://anlun-oss.oss-cn-shenzhen.aliyuncs.com/alun-java-interview/25_redis%E5%A6%82%E4%BD%95%E9%80%9A%E8%BF%87master%E6%A8%AA%E5%90%91%E6%89%A9%E5%AE%B9%E6%94%AF%E6%92%911T%2B%E6%95%B0%E6%8D%AE%E9%87%8F%E7%9A%84%E5%89%AF%E6%9C%AC.png)



![25_一致性hash算法的讲解和优点的副本](http://anlun-oss.oss-cn-shenzhen.aliyuncs.com/alun-java-interview/25_%E4%B8%80%E8%87%B4%E6%80%A7hash%E7%AE%97%E6%B3%95%E7%9A%84%E8%AE%B2%E8%A7%A3%E5%92%8C%E4%BC%98%E7%82%B9%E7%9A%84%E5%89%AF%E6%9C%AC.png)

![25_一致性hash算法的虚拟节点实现负载均衡的副本](http://anlun-oss.oss-cn-shenzhen.aliyuncs.com/alun-java-interview/25_%E4%B8%80%E8%87%B4%E6%80%A7hash%E7%AE%97%E6%B3%95%E7%9A%84%E8%99%9A%E6%8B%9F%E8%8A%82%E7%82%B9%E5%AE%9E%E7%8E%B0%E8%B4%9F%E8%BD%BD%E5%9D%87%E8%A1%A1%E7%9A%84%E5%89%AF%E6%9C%AC.png)



![25_最老土的hash算法以及弊端的副本](http://anlun-oss.oss-cn-shenzhen.aliyuncs.com/alun-java-interview/25_%E6%9C%80%E8%80%81%E5%9C%9F%E7%9A%84hash%E7%AE%97%E6%B3%95%E4%BB%A5%E5%8F%8A%E5%BC%8A%E7%AB%AF%E7%9A%84%E5%89%AF%E6%9C%AC.png)

![25_redis cluster hash slot算法的副本](http://anlun-oss.oss-cn-shenzhen.aliyuncs.com/alun-java-interview/25_redis%20cluster%20hash%20slot%E7%AE%97%E6%B3%95%E7%9A%84%E5%89%AF%E6%9C%AC.png)

![25_集中式的集群元数据存储和维护的副本](http://anlun-oss.oss-cn-shenzhen.aliyuncs.com/alun-java-interview/25_%E9%9B%86%E4%B8%AD%E5%BC%8F%E7%9A%84%E9%9B%86%E7%BE%A4%E5%85%83%E6%95%B0%E6%8D%AE%E5%AD%98%E5%82%A8%E5%92%8C%E7%BB%B4%E6%8A%A4%E7%9A%84%E5%89%AF%E6%9C%AC.png)

![25_gossip协议维护集群元数据的副本](http://anlun-oss.oss-cn-shenzhen.aliyuncs.com/alun-java-interview/25_gossip%E5%8D%8F%E8%AE%AE%E7%BB%B4%E6%8A%A4%E9%9B%86%E7%BE%A4%E5%85%83%E6%95%B0%E6%8D%AE%E7%9A%84%E5%89%AF%E6%9C%AC.png)





1、面试题

 

redis集群模式的工作原理能说一下么？在集群模式下，redis的key是如何寻址的？分布式寻址都有哪些算法？了解一致性hash算法吗？

 

2、面试官心里分析

 

在以前，如果前几年的时候，一般来说，redis如果要搞几个节点，每个节点存储一部分的数据，得借助一些中间件来实现，比如说有codis，或者twemproxy，都有。有一些redis中间件，你读写redis中间件，redis中间件负责将你的数据分布式存储在多台机器上的redis实例中。

 

这两年，redis不断在发展，redis也不断的有新的版本，redis cluster，redis集群模式，你可以做到在多台机器上，部署多个redis实例，每个实例存储一部分的数据，同时每个redis实例可以挂redis从实例，自动确保说，如果redis主实例挂了，会自动切换到redis从实例顶上来。

 

现在redis的新版本，大家都是用redis cluster的，也就是redis原生支持的redis集群模式，那么面试官肯定会就redis cluster对你来个几连炮。要是你没用过redis cluster，正常，以前很多人用codis之类的客户端来支持集群，但是起码你得研究一下redis cluster吧。

 

3、面试题剖析