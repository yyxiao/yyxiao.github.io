---
bg: "tools.jpg"
layout: post
title:  Prometheus+Grafana服务监控
crawlertitle: "Spring"
summary: "Spring Cloud"
date: 2019-06-05 10:01:00
categories: posts
tags: ['Java']
author: Xander
---

近期完成某项目技术架构设计，为了项目顺利实施，我抽出一定时间去尝试突破一些技术难点（业界较新，公司没人采用的技术）。


### Prometheus

```text
Prometheus是一套开源的系统监控、报警、时间序列数据库的组合，最初由SoundCloud开发，后来随着越来越多公司使用，于是便独立成开源项目。
我们常用的Kubernetes容器集群管理中，通常会搭配Prometheus一起来进行监控。Prometheus 基本原理是通过Http协议周期性抓取被监控组件的状态，
而输出这些被监控的组件的Http接口为Exporter，现在各个公司常用的Exporter都已经开源了，可以直接安装使用，如haproxy_exporter、blockbox_exporter、
mysqld_exporter、node_exporter 等等，更多支持的组件可点击下方传送门。
```
[传送门](https://github.com/prometheus)
    
    安装配置方法请自行百度、google，建议google很多问题资料在国内搜索不到。

    * 本机默认访问地址：http://localhost:9090/graph
    * Prometheus会将自己作为一个服务节点进行监控，监控信息访问地址：http://localhost:9090/metrics

[![1]({{ site.images }}/post/19/1.png)]({{ site.images }}/post/19/1.png)
[![4]({{ site.images }}/post/19/4.png)]({{ site.images }}/post/19/4.png)

### Grafana

```text
Grafana 是一个可视化仪表盘，它拥有美观的图标和布局展示，功能齐全的仪表盘和图形编辑器，默认支持 CloudWatch、Graphite、Elasticsearch、
InfluxDB、Mysql、PostgreSQL、Prometheus、OpenTSDB 等作为数据源。我们可以将 Prometheus 抓取的数据，通过 Grafana 优美的展示出来，非常直观。
```

    * 本机默认访问地址：http://localhost:3000
    * 官方仓库开源很多监控Dashboards，可以自行选择搭配
        
[![2]({{ site.images }}/post/19/2.png)]({{ site.images }}/post/19/2.png)
[![3]({{ site.images }}/post/19/3.png)]({{ site.images }}/post/19/3.png)

踩坑尝试

#### No datapoints found.

国内百度查出资料提示，系统时间有误；各种尝试换时间、时区，还是没有解决该问题。使用google查询该问题，发现是没有运行相对应的export，
或没有使用Prometheus集成export，数据没有采集到。

解决办法：
```text
引入相对应export，mysqld_exporter、node_exporter等，运行并使用Prometheus监控数据采集exporter。
```

[![5]({{ site.images }}/post/19/5.png)]({{ site.images }}/post/19/5.png)