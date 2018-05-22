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
```html
<div class="n-songtb"> 
       <div class="u-title u-title-1 f-cb"> 
        <h3> <span class="f-ff2">歌曲列表</span> </h3> 
        <span class="sub s-fc3"><span id="playlist-track-count">166</span>首歌</span> 
        <div class="more s-fc3">
         播放：
         <strong id="play-count" class="s-fc6">65</strong>次
        </div> 
        <div class="out out-list s-fc3"> 
         <i class="u-icn u-icn-95 f-fl"></i> 
         <a data-action="outchain" data-href="/outchain/0/362498513/" class="des s-fc7">生成外链播放器</a> 
        </div> 
       </div> 
       <div id="song-list-pre-cache" data-key="track_playlist-362498513" data-simple="1" data-pvnamed="1"> 
        <div class="u-load s-fc4">
         <i class="icn"></i> 加载中...
        </div> 
        <ul class="f-hide">
         <li><a href="/song?id=67572">婚礼的祝福</a></li>
         <li><a href="/song?id=1380636">Everytime We Touch</a></li>
         <li><a href="/song?id=36496004">相爱一场 (完整版)</a></li>
         <li><a href="/song?id=523251118">说散就散</a></li>
         <li><a href="/song?id=17057974">Everytime We Touch</a></li>
         <li><a href="/song?id=483671599">追光者</a></li>
         <li><a href="/song?id=31134194">如果有一天</a></li>
         <li><a href="/song?id=25645594">와</a></li>
         <li><a href="/song?id=307737">现在才明白</a></li>
         <li><a href="/song?id=21038694">Bad Romance</a></li>
         <li><a href="/song?id=179768">心碎(粤)</a></li>
         <li><a href="/song?id=28029509">咱们结婚吧</a></li>
         <li><a href="/song?id=29814898">可惜没如果</a></li>
         <li><a href="/song?id=25657148">听海</a></li>
         <li><a href="/song?id=280175">征服</a></li>
         <li><a href="/song?id=145586">拯救</a></li>
     </ul>
 </div>
```

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








