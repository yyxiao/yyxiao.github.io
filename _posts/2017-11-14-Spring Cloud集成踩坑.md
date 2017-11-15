---
bg: "tools.jpg"
layout: post
title:  Spring Boot 搭配踩坑
crawlertitle: "Spring"
summary: "Spring Cloud"
date: 2017-11-14 10:01:00
categories: posts
tags: ['Java']
author: Xander
---

看近年好多Dubbo集成的微服务都迁移到Spring Cloud，故研究搭建一下Spring Cloud。

```text
个人理解Spring Cloud其实是一个统称，是许多子项目的集合，这些子项目或多或少服务于spring Boot，协助搭建集成微服务。 
```

###坑点

* [FilterRegistrationBean从springboot的1.3.5到1.4.10的变化] 

```text
在1.4.0的时候，包名从org.springframework.boot.context.embedded.FilterRegistrationBean变为了
import org.springframework.boot.web.servlet.FilterRegistrationBean需要注意一下。

老夫在使用org.springframework.boot 为1.5.8.RELEASE版本，org.springframework.cloud使用Brixton.RELEASE版本时，
遇到FilterRegistrationBean找不到的问题，查看资源才发现1.4以后包地址进行了变化。
```

1. 搭配完成的eureka，相当于dubbo-admin页面。
[![1]({{ site.images }}/post/1711/1.png)]({{ site.images }}/post/1711/1.png)

2. 如果服务掉线，eureka会进行警示提醒。
[![2]({{ site.images }}/post/1711/2.png)]({{ site.images }}/post/1711/2.png)

3. 创建Rest接口时，在Controller类忘记添加注解@RestController
[![3]({{ site.images }}/post/1711/3.png)]({{ site.images }}/post/1711/3.png)










