---
title: "python中maketrans和translate的用法"
layout: post
comments: yes
---

刚开始看《Python Cookbook》，第一章是有关字符串操作的，其中第一章第八节出现了'translate'和'maketrans'，有点不懂，遂上网查，得到如下一篇blog。

转载自 [真心到永远的百度空间](http://hi.baidu.com/mengjingchao11/item/5e6c2afffe74491ecf9f323a)

###案例1.
首先说下maketrans函数是生成一个翻译表，比如将‘abc',按照顺序翻译成'ABC'，就可以这样写
 
`import string`

`t=string.maketrans('abc','ABC')`

将字符'a'->'A','b'->'B','c'->'C'。
然后使用translate函数
`’abc123‘.translate(t,'123')`。translate函数的第一个参数要求是翻译表，这里为之前定义的t，然后使用第二个参数将’123‘从字符串’abc123‘中过滤掉。
那么translate的执行顺序是：先从字符串只过滤掉第二个参数的字符，然后对过滤后的字符串进行t所示的翻译。结果为：ABC

###案例2.
现在我想过滤字符串中不属于指定集合的字符。
给定一个需要保留的字符串的集合，构建一个过滤函数，并可将其应用于字符串，返回一个s的拷贝，该拷贝只含指定字符集合的元素
首先定义一个翻译表，指明’无需翻译‘，`allchars=string.maketrans('','')`
  `delchars=allchars.translate(allchars,'meng')`delchars包含了除’meng‘之外的所有字符。
然后就可以使用translate函数来完成。
 `’me32n315g123‘.translate(allchars,delchars)`就会返回meng字符串。