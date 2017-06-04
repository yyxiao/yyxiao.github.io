---
bg: "tools.jpg"
layout: post
title:  Spring Boot 搭配踩坑
crawlertitle: "Spring"
summary: "Spring Boot"
date: 2017-06-04 10:01:00
categories: posts
tags: ['Java']
author: Xander
---

考完信息系统项目管理师后自己一度感到迷茫，不知道自己应该是否转型，选择技术架构还是项目管理，足足纠结好几个月后，老夫发现貌似不用那么纠结，
可以继续研究技术，然后提高自己的管理、交流水平。

[![1]({{ site.images }}/post/170604/1.png)]({{ site.images }}/post/170604/1.png)

###坑点

* [com.alibaba.druid.pool.vendor.MySqlValidConnectionChecker] 

```text
Cannot resolve com.mysq.jdbc.Connection.ping method.  Will use 'SELECT 1' instead.

好吧，其实也是自己闲得无聊，非要使用druid连接池，明显阿里druid与mysql链接报错，老夫刚开始mysql使用6.0.2的jar包，
后换到5.1.38后问题解决。ps：好奇怪高版本不兼容。
```




