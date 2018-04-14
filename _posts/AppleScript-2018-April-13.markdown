---
layout: post
title: 心情不好，拿appleScript开个刀
categories: funTool
description: 这是你被浪费的时间
keywords: auto workflow
---

## 事出有因
学习appleScript是最近迷上了workflow系列，工作效率的提升都在这一些细节中，比如iOS中的workflow，Android的tasker，OSX的自动操作，都能帮我们解决生活中很多问题，让大脑主要负责逻辑的任务，而不是控制肌肉的重复，仿佛一个傀儡。那么今天的applescript为我们解决了什么问题呢，今天我们就来说一下这篇博客是如何造出来的，

![MDHeader](../image/appleScript/MDHeader.png)

    
每一篇jekyll博客都需要有一个头部，然后才开始写作，你不用管这个头部干嘛用的，只需要知道每一篇文章都需要有这个东西就好了，那在写之前我需要几步呢，

#### 之前的方式
1. 打开软件<br> ![macdown](../image/appleScript/macDownIcon.png)
2. 对博客进行命名，文件名会有写作当天日期<br> ![unname](../image/appleScript/unname.png)
3. 寻找我之前在某个地方存的模板文件，复制粘贴到我现在的编辑页面中，<br> ![jekylltemplate](../image/appleScript/Jekylltemplate.png)

在现在看来，这几步都还好，没多麻烦，但是请注意，惰性是科技进步的初动力，我就是懒到这个地步了，如果能用点一个按钮的时间都做好这些事岂不是更好。“代码”，让生活更简单。













### show time
这是<font color=#609900>developer.apple</font>对AppleScript的定义

>AppleScript is a scripting language created by Apple. It allows users to directly control scriptable Macintosh applications, as well as parts of macOS itself. You can create scripts—sets of written instructions—to automate repetitive tasks, combine features from multiple scriptable applications, and create complex workflows.<br>


这是一个很简单但是灵性的脚本语言，他的语法简单到几乎可能大概好像也许就是自然语言。比如`say "nice to meet you"` 这个指令告诉siri说nice to meet you;再比如 `set name to value`,表示将name这个变量的值设置为value;`beep` 就是电脑发声。

	tell application "MacDown"
		make new document
		set text of front document to "---
	layout: post
	title: template page
	categories: [cate1, cate2]
	description: some word here
	keywords: keyword1, keyword2
	---"
		set today to current date
		set datename to "/Users/shadow/prog/blog_gitpage/_posts/" & year of today & "-" & month of today & "-" & day of today
		save front document in datename as Markdown
		say "创建成功了"
	end tell
	
好了写完了，demo程序已经实现它该有的基本功能了，而且成功后还语音提示你，感觉还是很周到的，我们多考虑一下鲁棒性，文件如果已经存在的话是不是就会重复创建，并覆盖掉之前的文件，这将是一个很可怕的问题，所以我们需要加上验重操作，这就带出我们的第二个问题，创建对象的操作应该放在验重通过后，这样能保证更好的稳定性。

	tell application "MacDown"
		set today to current date
		set datename to "/Users/shadow/prog/blog_gitpage/_posts/" & year of today & "-" & month of today & "-" & day of today
		tell application "System Events" to set fileExists to exists disk item (my POSIX file datename as string)
		if fileExists then
			say "文件已经存在了"
		else
			make new document at front
			set text of front document to "---
	layout: post
	title: template page
	categories: [cate1, cate2]
	description: some word here
	keywords: keyword1, keyword2
	---"
			save front document in datename as Markdown
			say "创建成功了"
		end if
	end tell
	 
## the end

暂时写到这里吧，早点休息，好好生活。原谅我一年没写代码了，只能拿这个找存在感了。
<br><br><br>
## 骗人的
你以为再见了吗，别着急，我从来都不按套路出牌，刚睡醒接着写，你还可以做一些小动作显得逼格更高一点，在applescript编辑器左上角找`文件`->`导出` <br>
选`应用程序`<br> ![jekyllApplet](../image/appleScript/jekyllApplet.png) 
&emsp;这个时候你在finder中看到了你要的脚本，可是有点丑，而且要是写多几个脚本放在一个目录下，会看的眼晕，所以我们现在给他换个图标，首先找到你的图标，格式貌似有三种，我一般用png，[font awesome](https://fontawesome.com/icons)里面有很多好看的图标，而且开源，保存在本地打开<br> 如图所示在预览中将图标全部选择![](../image/appleScript/jekyllIcon.png)

右键图标，进入`显示简介`<br>![jekyllSetting](../image/appleScript/jekyllSetting.png)

![jekyllContent](../image/appleScript/jekyllContent.png)<br>
点击上图的图标然后`command+v`,
最后拖到应用程序文件夹里就能在lunchpad里面使用了。<br>
![jekyllFinal](../image/appleScript/jekyllFinal.png)<br>
这个方式可以把你的所有文件夹都改成有趣的图标，不用再看文件名了。<br>
DengDengDeng
![desktop](../image/deskTop.png)