---
layout:     post
title:      Oracle 存储过程小记
date:       2016-08-29 21:35:18
summary:    Oracle 存储过程
categories: Oracle SQL
thumbnail: Oracle
author: "shadow"
tags:
 - Oracle
 - SQL
 - shadow grand
---

#### 定义

**储存程序** (Stored Procedure)，又可称预储程序或者存储过程，是一种在数据库中存储复杂程序，以便外部程序调用的一种[数据库对象](https://zh.wikipedia.org/w/index.php?title=%E8%B3%87%E6%96%99%E5%BA%AB%E7%89%A9%E4%BB%B6&action=edit&redlink=1)，它可以视为数据库中的一种函数或子程序。(来自维基百科，*不服你来打我呀*)

#### 0x00问题提出

首先是一个存储过程中字符串内容的过滤，（问题描述：在一个字符串中出现了一个超链接，而现在希望将其连接标签去掉，只保留文字。）思路很简单，直接反应到正则表达式匹配然后删除。

那么**问题**来了  怎么在存储过程中应用正则表达式。

#### 0x01Oracle正则表达式分析

Oracle中使用正则表达式通过这四个函数，通过指定要处理的文本和提前编辑好的模式（pattern）完成特定的功能。

现在列举解释这个四个函数：

- regexp_like 


- regexp_substr


- regexp_instr


- regexp_replace

1. regexp_like(experssion, pattern) 返回一个布尔值  和like类似 通过正则表达式匹配内容。
2. regexp_substr 函数 拾取符合正则式描述的字符串。返回子字符串。
3. regexp_instr(source_string,pattern[,position[,occurrence[,return_option[,match_paramter]]]]) 用于按照特定样式确定子串在字符串中的位置。source_string 为源字符串，pattern 为指定正则式，position（optional） 指定其实地址，occurence(可选)用于指定第n次出现的子串，match_parameter(optional) 用于指定样式匹配修饰符。 
4. regexp_replace(source_string,pattern[,replace_string[,position[,occurence[,match_parameter]]]]) :这是本次任务使用的函数，通过指定字符串和正则式 替换目标串为指定串。 例如regexp_parameter ('shadow world9','[0-9]','i')  得到就是将“shadow world9 ”中的数字9 替换为“i”

 所以回到任务  肯定都知道策略了，只要匹配到链接标签，然后将其替换为空就可以做到删除过滤了。可以知道链接的形式一般为"<a href="http://www.something.com">word display</a>" 那么"<a.*?a>" 这一模式就能匹配所有的超链接了（特殊情况考虑不多，，，将就下）

#### 0x02正则表达式再练 

最近想到一个点子，把平常的正则式例子放在这里，大家感兴趣的可以一起讨论一下，看看哪里还能改进，希望大神们不吝赐教。

##### 	00 

今晚累了，先更在这里吧。立下flag！！！