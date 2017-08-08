---
bg: "tools.jpg"
layout: post
title:  AnypointStudio初学
crawlertitle: "Anypoint Studio"
summary: "学习Anypoint Studio"
date: 2017-08-08 09:27:00
categories: posts
tags: ['Tools']
author: Xander
---

老夫最近实现甘肃省统一认证平台需要做一些供外部调用的接口，架构组指定规范使用技术为 mule ESB，老夫第一次听到这个词，
故需要扫扫盲。

### 什么是mule？

Mule（www.mulesoft.org）是企业服务总线的一个最优秀的开源实现之一。它是一个以Java为核心的轻量级的消息框架和整合平台，
允许开发人员快速便利地连接多个应用，并支持应用间的数据交换。它支持集成现有系统而无论其底层采用何种技术，
如JMS、WebServices、JDBC、HTTP以及其他技术。Mule通过Transports/Connectors与外围的异构系统连接，
提供Routing（路由）、TransactionManagement(事务管理）、Transfor-mation（转换）、MessageBroker（消息代理）、
TransportationManagement（传输管理）、Security（安全）等核心模块。外围系统的服务请求通过MuleESB的Transport接入，
MuleESB通过Transformer进行数据的格式转换，然后经过InboundRouter进行消息过滤（内部通过配置filter实现）
后交给Mule的Com-ponent等进行业务逻辑处理。处理后的结果通过OutboundRouter确定传递给哪个接收方，
然后通过Transformer进行数据格式转换，再通过Transport连接至接收方。


### 什么是ESB？

ESB全称为Enterprise Service Bus，即企业服务总线。它是传统中间件技术与XML、Web服务等技术结合的产物。
ESB提供了网络中最基本的连接中枢，是构筑企业神经系统的必要元素。ESB的出现改变了传统的软件架构，
可以提供比传统中间件产品更为廉价的解决方案，同时它还可以消除不同应用之间的技术差异，让不同的应用服务器协调运作，
实现了不同服务之间的通信与整合。从功能上看，ESB提供了事件驱动和文档导向的处理模式，以及分布式的运行管理机制，
它支持基于内容的路由和过滤，具备了复杂数据的传输能力，并可以提供一系列的标准接口。

```text
MuleESB是一个企业服务总线(ESB)消息框架。MuleESB是一个消息框架，用于程序之间的数据交换。程序或应用被封装成为服务，
服务包含服务组件、消息路由和其它一些配置。Transport使得服务间的数据在不同渠道内得以传送，
并且transport在对数据的传输过程中，对需要格式转换的数据进行数据转换。
```

### 下载和安装

网上资料大都建议安装Mule Studio，但登上Mule官网后并没有Mule Studio下载地址，原来mule在发展一段时间后将Mule Studio合并到
Anypoint Studio中，它是基于Eclipse的，和Eclipse差不多，很容易上手。它是一个 Mule ESB 可视化设计工具。支持图形化组件拖拽，
直接编辑消息流，从而不用在编写大量的XML配置文件。个人感觉其实更像IDEA多一些。

[![1]({{ site.images }}/post/1708/1.png)]({{ site.images }}/post/1708/1.png)


