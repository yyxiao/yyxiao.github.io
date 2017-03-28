---
bg: "tools.jpg"
layout: post
title:  Java_split使用常见问题
crawlertitle: "Java split()"
summary: "split()"
date: 2017-03-28 10:46:00
categories: posts
tags: ['JAVA']
author: Xander
---

老夫最近使用idea进行代码优化时，发现新公司project中一些问题，比如使用split()进行分隔时没有按照特定业务场景进行使用。

```Java
String[] licesses = licesse.split("#",7);
```

Java中可以使用split将字符串按照指定的分割符进行分隔，然后return字符串数组。

### split方法

stringObj.split([separator，[limit]]) 
* stringObj
    必选项。要被分解的 String 对象或文字,该对象不会被split方法修改。
* separator 
    可选项。字符串或正则表达式对象，它标识了分隔字符串时使用的是一个还是多个字符。如果忽略该选项，返回包含整个字符串的单一元素数组。 
* limit
     参数控制模式应用的次数，因此影响所得数组的长度。如果该限制 n 大于 0，则模式将被最多应用 n - 1 次，数组的长度将不会大于 n，
     而且数组的最后一项将包含所有超出最后匹配的定界符的输入。如果 n 为非正，那么模式将被应用尽可能多的次数，而且数组可以是任何长度。
     如果 n 为 0，那么模式将被应用尽可能多的次数，数组可以是任何长度，并且结尾空字符串将被丢弃。


#### 源码如下：
```Java
public String[] split(String regex, int limit) {
    /* fastpath if the regex is a
     (1)one-char String and this character is not one of the
        RegEx's meta characters ".$|()[{^?*+\\", or
     (2)two-char String and the first char is the backslash and
        the second is not the ascii digit or ascii letter.
     */
    char ch = 0;
    if (((regex.value.length == 1 &&
         ".$|()[{^?*+\\".indexOf(ch = regex.charAt(0)) == -1) ||
         (regex.length() == 2 &&
          regex.charAt(0) == '\\' &&
          (((ch = regex.charAt(1))-'0')|('9'-ch)) < 0 &&
          ((ch-'a')|('z'-ch)) < 0 &&
          ((ch-'A')|('Z'-ch)) < 0)) &&
        (ch < Character.MIN_HIGH_SURROGATE ||
         ch > Character.MAX_LOW_SURROGATE))
    {
        int off = 0;
        int next = 0;
        boolean limited = limit > 0;
        ArrayList<String> list = new ArrayList<>();
        while ((next = indexOf(ch, off)) != -1) {
            if (!limited || list.size() < limit - 1) {
                list.add(substring(off, next));
                off = next + 1;
            } else {    // last one
                //assert (list.size() == limit - 1);
                list.add(substring(off, value.length));
                off = value.length;
                break;
            }
        }
        // If no match was found, return this
        if (off == 0)
            return new String[]{this};

        // Add remaining segment
        if (!limited || list.size() < limit)
            list.add(substring(off, value.length));

        // Construct result
        int resultSize = list.size();
        if (limit == 0)
            while (resultSize > 0 && list.get(resultSize - 1).length() == 0)
                resultSize--;
        String[] result = new String[resultSize];
        return list.subList(0, resultSize).toArray(result);
    }
    return Pattern.compile(regex).split(this, limit);
}
```

#### 常见使用split

[![1]({{ site.images }}/post/170328/1.png)]({{ site.images }}/post/170328/1.png)

[![2]({{ site.images }}/post/170328/2.png)]({{ site.images }}/post/170328/2.png)

#### 当设置limit参数
    
[![3]({{ site.images }}/post/170328/3.png)]({{ site.images }}/post/170328/3.png)

[![4]({{ site.images }}/post/170328/4.png)]({{ site.images }}/post/170328/4.png)

```text
1. 如果用“.”作为分隔的话,必须是如下写法,String.split("\\."),这样才能正确的分隔开,不能用String.split(".");
2. 如果用“|”作为分隔的话,必须是如下写法,String.split("\\|"),这样才能正确的分隔开,不能用String.split("|");
```

