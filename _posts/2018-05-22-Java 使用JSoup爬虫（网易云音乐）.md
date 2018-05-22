---
bg: "tools.jpg"
layout: post
title:  Jsoup爬虫网易云音乐
crawlertitle: "Java"
summary: "Jsoup"
date: 2018-05-22 9:01:00
categories: posts
tags: ['Java']
author: Xander
---

忙里偷闲，最近老夫刚入手一辆SUV，开车的时候想听听音乐，又不想浪费流量，使用网易云音乐客户端下载自己的歌单都下载不了，
这怎么可以忍，作为一个技术控，果断需要自己将喜欢的歌曲下载下来。


### 选择环境

```text
17年玩过Python2.7(3、5)，使用pyspider爬取某站一些可用数据；但技术控必须得不断挑战自己，尝试不同的技术，
故这次选择Java8，使用Jsoup来爬取网易云音乐歌单列表，需引入jsoup.jar，因为第一次使用Jsoup，接下来步骤区分明细一些。
```

* 获取请求连接
```java
Connection con = Jsoup.connect("http://music.163.com/playlist?id=相对应歌单id");
```

* 把String转化成document格式
```java
Document doc = con.header("Referer", "http://music.163.com/").get();
```

* * 上步得到结果doc,选截部分：

[![4]({{ site.images }}/post/18/01/4.png)]({{ site.images }}/post/18/01/4.png)

* 获取所有符合条件的节点集
```java 
Elements elements = doc.select("ul[class=f-hide] a");
```

* 使用java8中的stream，更便捷的操作collection
```java 
elements.stream().forEach(w->maps.put(w.text(),w.attr("href")));
```

* * maps结果为：

[![3]({{ site.images }}/post/18/01/3.png)]({{ site.images }}/post/18/01/3.png)

然后爬取http://music.163.com/+song?id=145586，获取相对应页面的.mp3结尾的url，循环download，具体步骤不进行描述了。

部分代码如下：
```java 
public static void main(String[] args) throws Exception {
        Map<String,String> maps = new HashMap<>();
        //获取请求连接
        Connection con = Jsoup.connect("http://music.163.com/playlist?id=362498513");
        //把String转化成document格式
        Document doc = con.header("Referer", "http://music.163.com/").header("Host", "music.163.com").get();
        //获取所有符合条件的节点集
        Elements elements = doc.select("ul[class=f-hide] a");

        //使用java8stream、forEach将数据放入maps
        elements.stream().forEach(w->maps.put(w.text(),w.attr("href")));
    }
```








