---
layout:     post
title:      selenium
date:       2017-09-10 21:35:18
summary:    tech
categories: framework
thumbnail: selenium
author: "shadow"
tags:
 - selenium
 - shadow grand
---

## 框架介绍
selenium 是个很好的web自动化测试框架，通过和webdriver进行交互，对浏览器进行操作，对于chrome IE Firefox（火狐是原生支持，虽然我也不知道啥意思） 都有很好支持，chrome是我最为钟爱的浏览器，今天就用chrome作为展示对象，安装并使用selenium。   

## 安装

1. 首先我们需要Python的包管理器 `pip`   
通过[wget](https://bootstrap.pypa.io/get-pip.py) 获得pip.py这个文件   
然后通过Python 运行进行pip安装。
![get pip](/image/selenium/get_pip.png) 
如上就完成了pip的安装
![pip not install](/image/selenium/pip_notinstall.png)
这里就引入了一个问题，pip的安装，mac下第一次安装pip有可能会产生抑制安装不上的问题，一直会报一个权限问题，无论是sudo 还是su 各种姿势都无法规避这个问题的时候大家需要考虑一下apple的SIP 功能需要关闭了（网上搜索会有很多解决方案，不是本次博客聚焦内容）
2. 接着是安装selenium框架，很方便的指令就能完成，这步一般不会出现问题，至少我没有      
![get selenium](/image/selenium/install_selenium.png)
3. 最后就是完成验证部分 首先进入Python CLI `help（“modules”）`进行验证。   
![help modules](/image/selenium/help_selenium.png)
4. 如果通过第三步，那么就可以进行使用测试了   
![dw](/image/selenium/click_selenium.png)
![click browser](/image/selenium/click_browser.png)

