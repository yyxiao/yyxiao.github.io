---
bg: "tools.jpg"
layout: post
title:  Spring Cloud 搭配踩坑
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

### spring cloud子项目包括：

```text
* Spring Cloud Config：配置管理开发工具包，可以让你把配置放到远程服务器，目前支持本地存储、Git以及Subversion。
* Spring Cloud Bus：事件、消息总线，用于在集群（例如，配置变化事件）中传播状态变化，可与Spring Cloud Config联合实现热部署。
* Spring Cloud Netflix：针对多种Netflix组件提供的开发工具包，其中包括Eureka、Hystrix、Zuul、Archaius等。
* Netflix Eureka：云端负载均衡，一个基于 REST 的服务，用于定位服务，以实现云端的负载均衡和中间层服务器的故障转移。
* Netflix Hystrix：容错管理工具，旨在通过控制服务和第三方库的节点,从而对延迟和故障提供更强大的容错能力。
* Netflix Zuul：边缘服务工具，是提供动态路由，监控，弹性，安全等的边缘服务。
* Netflix Archaius：配置管理API，包含一系列配置管理API，提供动态类型化属性、线程安全配置操作、轮询框架、回调机制等功能。
* Spring Cloud for Cloud Foundry：通过Oauth2协议绑定服务到CloudFoundry，CloudFoundry是VMware推出的开源PaaS云平台。
* Spring Cloud Sleuth：日志收集工具包，封装了Dapper,Zipkin和HTrace操作。
* Spring Cloud Data Flow：大数据操作工具，通过命令行方式操作数据流。
* Spring Cloud Security：安全工具包，为你的应用程序添加安全控制，主要是指OAuth2。
* Spring Cloud Consul：封装了Consul操作，consul是一个服务发现与配置工具，与Docker容器可以无缝集成。
* Spring Cloud Zookeeper：操作Zookeeper的工具包，用于使用zookeeper方式的服务注册和发现。
* Spring Cloud Stream：数据流操作开发包，封装了与Redis,Rabbit、Kafka等发送接收消息。
* Spring Cloud CLI：基于 Spring Boot CLI，可以让你以命令行方式快速建立云组件。
```

### 坑点

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










