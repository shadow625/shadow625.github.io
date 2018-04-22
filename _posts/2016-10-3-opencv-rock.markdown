---
layout: post
title: android  opencv
categories: [android, opencv]
description: some word here
keywords: keyword1, keyword2
---


## 今天安装测试了Android下的opencv，大致理解整体过程。

首先安装opencv manager 这是一个将JAVA翻译native语言的过程工具，我们通过调用opencv JAVA API去实现响应的功能。

通过自定义的view，opencv可以展示改变后的相机传输的内容。我们通过FrameLayout加入了一个TextView方便以后显示照片上的手指数量。

​	CameraBridgeViewBase这是用来把信息传给manager并接收展示来自manager的图形。

​	onCameraViewStarted 每当摄像头打开时，这个方法就被调用。

​	onCameraFrame抓帧然后进行分析。

对于Android opencv实现的资料较少，无法获取更多内容。正在尝试C++下