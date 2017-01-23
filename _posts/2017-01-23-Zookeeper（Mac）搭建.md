---
bg: "tools.jpg"
layout: post
title:  Zookeeper（Mac）搭建
crawlertitle: "build Zookeeper"
summary: "Zookeeper"
date: 2017-01-23 15:09:00
categories: posts
tags: ['Tools']
author: Xander
---

首先需要搭建本地JAVA（JDK）环境，然后才可以搭建Zookeeper框架。

```text
zookeeper在mac常见两种搭建方式，一种为下载压缩包进行搭建，另一种为使用brew安装。
本文使用压缩包进行安装
ps：强迫症患者不太习惯傻瓜式安装
```

### 1. 下载Zookeeper

`下载地址： http://www.apache.org/dyn/closer.cgi/zookeeper`

首先从官网下载zookeeper压缩吧，然后解压文件:

`tar zxvf zookeeper-3.4.9.tar.gz`

### 2. 编辑配置文件

在zookeeper-3.4.9/conf目录下，有zoo_sample.cfg，我们直接cp一份，并修改：

```text
#tickTime: zookeeper中使用的基本时间单位, 毫秒值.
#dataDir: 数据目录. 可以是任意目录.
#dataLogDir: log目录, 同样可以是任意目录. 如果没有设置该参数, 将使用和#dataDir相同的设置.
#clientPort: 监听client连接的端口号.
```

### 3. 配置环境变量

习惯性将软件移动到一起，windows继承来的习惯，所以mv到/usr/local/bin/zookeeper，然后自己又比较懒，不太想每次cd到这么深的目录，所以配置环境变量。

`vim .bash_profile`

`source .bash_profile`

### 4. 运行Zookeeper

```text
zkServer.sh start   运行
zkServer.sh stop    停止
zkCli.sh            客户端
```

[![1]({{ site.images }}/post/170123/1.jpeg)]({{ site.images }}/post/170123/1.jpeg)

[![2]({{ site.images }}/post/170123/2.png)]({{ site.images }}/post/170123/2.png)
