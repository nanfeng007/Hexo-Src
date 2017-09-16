---
title: JAVA初级程序员进阶
date: 2017-08-19 06:13:12
tags: JAVA
categories: JAVA
---
<span class="RichText CopyrightRichText-richText" itemprop="text"><p>===========更新=====================</p><p>有人私信我说，除了要掌握的20%以外还要掌握些什么知识才能游刃有余。下面说说我接触（使用）过、的东西吧。</p><ol><li>java以分布式应用丰富的生态闻名，在分布式系统中逃不过CAP的抉择。早早了解一些分布式一致性协议paxos、raft等。学习zookeeper的原理和使用场景(metadata、分布式锁、leaderEletion... etc)</li><li>RPC框架在SOA架构中起着重要的作用，好好探究终是有好处的，在这里推荐阿里巴巴的dubbo框架，同时会netty、mina等网络库</li><li>Hadoop系列 Storm Spark  等离线\实时计算框架</li><li>ElasticSearch\SolrCloud 分布式搜索 ELK 日志相关的东西对这些比较敏感，当然在更多的场景使用ES也是有很多</li><li>消息队列 kafka\MetaQ RabbitMQ  缓存 Redis/memcached .容器tomcat/jetty web服务器NGINX/OpenResty</li><li>然后就是各种基础知识，编程语言、网络方面、数据库、数据结构和算法。不要觉得任何一项都精通了，敢说精通的知乎能有几个。</li><li>= =太多东西了，一时还真想不起来完。上面这些也就目前业内常见的东西吧,在不同的工作当中会遇到不同的问题，需要更多的工具、开源框架来解决各种蛋疼的问题。然后会的东西越来越多，然后就不知道自己到底会写什么了。先完，需要详细的私信我</li><li>掌握技能也就是需要时间成本和学习成本，要成为一个好的程序员不要怕学习，有学历能力需要新技术才能跟得上，想当年才学的时候struts2比springmvc高出一截，不过现在也基本没人用啦。</li></ol><br><br><p>============以下是原答案=======================</p><p>主要的一些库包括:</p><ul><li>commons-*(apache common库，包括常用IO，集合，网络，log等等等等，貌似至少有40+commons库吧，不过常用的也就那几个，详见<a href="https://link.zhihu.com/?target=https%3A//commons.apache.org/" class=" wrap external" target="_blank" rel="nofollow noreferrer">Apache Commons<i class="icon-external"></i></a>)</li><li>guava库 google出的，我最喜欢用这个工具库~，不过有些东西还是只有上面的commons库才有，比如LRUmap。不过guava有堆内cache</li><li>fastjson，操作json用的</li></ul><p>常用框架：
SpringMVC Mybatis Spring这些开发web最常用的,当然还会用RPC框架，可以参考Thrift dubbo gRPC等等</p><p>工具
git maven</p><p>常用的就这些吧，不常用的就不说了。看自己的工作内容了，当然也不是会了哪些就能找到工作，关键还是学习能力。有新技术能够在最短的时间内学会最好。说不定这些东西今年就淘汰了也说不定~</p></span>
