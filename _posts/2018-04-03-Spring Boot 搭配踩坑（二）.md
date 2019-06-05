---
bg: "tools.jpg"
layout: post
title:  Spring Boot 搭配踩坑（二）
crawlertitle: "Spring"
summary: "Spring Cloud"
date: 2018-04-03 10:01:00
categories: posts
tags: ['Java']
author: Xander
---

刚忙完一波某省统一身份认证系统设计、开发工作，可以稍微空闲学习一些自己喜欢的新知识了，继续spring cloud（eureka、hystrix）。


### Eureka

```text
云端服务发现，一个基于 REST 的服务，用于定位服务，以实现云端中间层服务发现和故障转移。
个人感觉相当于Dubbo-admin与zookeeper的集成。
```

### hystrix

```text
熔断器，容错管理工具，旨在通过熔断机制控制服务和第三方库的节点,从而对延迟和故障提供更强大的容错能力。
http://127.0.0.1:8101/hystrix
调用熔断器仪表盘 查看接口熔断情况
http://localhost:8101/hystrix/monitor?stream=http://localhost:9000/hystrix.stream
```

#### Unable to connect to Command Metric Stream.

* pom.xml需引入以下jar包：

方法一：
```xml
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-hystrix</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.cloud</groupId>
    <artifactId>spring-cloud-starter-hystrix-dashboard</artifactId>
</dependency>
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-actuator</artifactId>
</dependency>
```

[![1]({{ site.images }}/post/18/01/1.png)]({{ site.images }}/post/18/01/1.png)
 
#### springBoot接入swagger2：

* api列表中没有生成相对应的接口，需查看Swagger2类中
`apis(RequestHandlerSelectors.basePackage("#####"))`是否配置正确。

```xml
<dependency>
    <groupId>io.springfox</groupId>
    <artifactId>springfox-swagger2</artifactId>
</dependency>

<dependency>
    <groupId>io.springfox</groupId>
    <artifactId>springfox-swagger-ui</artifactId>
</dependency>
```



[![2]({{ site.images }}/post/18/01/2.png)]({{ site.images }}/post/18/01/2.png)

[MyBoot传送门](https://github.com/yyxiao/MyBoot)












