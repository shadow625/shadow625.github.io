---
layout:     post
title:      Android进程间通信	
date:       2016-05-05 12:32:18
summary:    some imformation about the UML
categories: Android
thumbnail: Android
author: "shadow"
tags:
 - thumbnails
 - shadow grand
---

### 进程间通信
作为Android系统中核心的需求，进程间通信显得尤为重要，今天我们从经典Linux的IPC实现说起，进一步分析Android进程间通信方式。

### 进程间通信经典实现
1.共享内存：
原理在于可以创建一个公共可访问的内存区域，两个进程通过这个共享的内存区域进行通讯，所谓的通信，就是变量的存取。例比于两个人通过一个邮箱进行接头，A将信息放置在邮箱中，并查看信箱中是否有自己需要的内容，B从信箱中取出A留下的信息，进行自己的活动。
	