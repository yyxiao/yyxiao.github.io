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

* 【** WARNING ** : Your ApplicationContext is unlikely to start due to a @ComponentScan of the default package.】

Your code is in the default package, i.e. you have .java files in src/main/java with no package statement at the top. 
There's a warning message in the log indicating that this is likely to cause problems:

`** WARNING ** : Your ApplicationContext is unlikely to start due to a @ComponentScan of the default package.`

You need to move your code into a package of its own. For example, move your .java files into src/main/java/com/example 
and add package com.example; to the top of each file.

因为application.java文件不能直接放在main/java文件夹下，必须要建一个包把它放进去。

* 使用外部容器报404

```
Spring Boot项目需要部署在外部容器中的时候，Spring Boot导出的war包如果直接在Tomcat的部署会报错。
```

* * 需做到：
1. 继承SpringBootServletInitializer
   外部容器部署的话，就不能依赖于Application的main函数了，而是要以类似于web.xml文件配置的方式来启动Spring应用上下文，
   此时我们需要在启动类中继承SpringBootServletInitializer并实现configure方法：
   
```java
    /**
     * 重写configure，相当于web.xml加载main
     * @Description @TODO
     * @author Xander
     * @Date 2017/10/26 下午3:43
     * The word 'impossible' is not in my dictionary.
     */
    @Override
    protected SpringApplicationBuilder configure(SpringApplicationBuilder application) {
        return application.sources(Application.class);
    }
```

这个类的作用与在web.xml中配置负责初始化Spring应用上下文的监听器作用类似，只不过在这里不需要编写额外的XML文件了。

2. pom.xml修改tomcat相关的配置
   如果要将最终的打包形式改为war的话，还需要对pom.xml文件进行修改，因为spring-boot-starter-web中包含内嵌的tomcat容器，
   所以直接部署在外部容器会冲突报错。这里有两种方法可以解决，如下：
   
方法一：
```xml
<dependency>
    <groupId>org.springframework.boot</groupId>
    <artifactId>spring-boot-starter-web</artifactId>
    <exclusions>
        <exclusion>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-tomcat</artifactId>
        </exclusion>
    </exclusions>
</dependency>
```

注：
在这里需要移除对嵌入式Tomcat的依赖，这样打出的war包中，在lib目录下才不会包含Tomcat相关的jar包，否则将会出现启动错误。
还有一个很关键的关键点，就是tomcat-embed-jasper中scope必须是provided。

```xml
<dependency>
    <groupId>org.apache.tomcat.embed</groupId>
    <artifactId>tomcat-embed-jasper</artifactId>
    <scope>provided</scope>
</dependency>
```
因为SpringBootServletInitializer需要依赖 javax.servlet，而tomcat-embed-jasper下面的tomcat-embed-core中就有这个javax.servlet，
如果没用provided，最终打好的war里面会有servlet-api这个jar，这样就会跟tomcat本身的冲突了。


[![2]({{ site.images }}/post/170604/2.png)]({{ site.images }}/post/170604/2.png)

注意配置idea

[![3]({{ site.images }}/post/170604/3.png)]({{ site.images }}/post/170604/3.png)










