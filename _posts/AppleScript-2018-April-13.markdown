---
layout: post
title: appleScript
categories: funTool
description: 这是你被浪费的时间
keywords: auto workflow
---

## 
事出有因，学习appleScript是最近迷上了workflow系列，工作效率的提升都在这一些细节中，今天我们就来说一下这篇博客是如何造出来的，

![MDHeader](../image/MDHeader.png)

    
每一篇jekyll博客都需要有一个头部，然后才开始写作，你不用管这个头部干嘛用的，只需要知道每一篇文章都需要有这个东西就好了，那在写之前我需要几步呢，

#### 之前的方式
1. 打开软件<br> ![macdown](../image/macDownIcon.png)
2. 对博客进行命名，文件名会有写作当天日期<br> ![unname](../image/unname.png)
3. 寻找我之前在某个地方存的模板文件，复制粘贴到我现在的编辑页面中，<br> ![jekylltemplate](../image/Jekylltemplate.png)

在现在看来，这几步都还好，没多麻烦，但是请注意，惰性是科技进步的初动力，我就是懒到这个地步了，如果能用点一个按钮的时间都做好这些事岂不是更好。“代码”，让生活更简单。













### show time
这是<font color=#609900>developer.apple</font>对AppleScript的定义

>AppleScript is a scripting language created by Apple. It allows users to directly control scriptable Macintosh applications, as well as parts of macOS itself. You can create scripts—sets of written instructions—to automate repetitive tasks, combine features from multiple scriptable applications, and create complex workflows.<br>


这是一个很简单但是灵性的脚本语言，他的语法简单到几乎可能大概好像也许就是自然语言。比如`say "nice to meet you"` 这个指令告诉siri说nice to meet you;再比如 `set name to value`,表示将name这个变量的值设置为value;`beep` 就是电脑发声。
