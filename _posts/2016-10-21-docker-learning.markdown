---
layout: post
title: docker-learning
categories: docker
description: docker playground
keywords: docker, container
---


### 首先docker在ubuntu下的安装。

看一下这个链接：https://docs.docker.com/engine/installation/linux/ubuntulinux/

我没用过，也就不知道中间的问题要怎么解决。

当安装好docker后可以使用import指令将现在的这个ubuntu.tar直接引入。（提前说一下 docker需要在超级权限下运行，所以你的docker指令最好是加一个sudo 或者直接su提权）

```
docker load < 
```

此处的 ubuntu.tar 就是我提供的文件名，因为在当前工作目录下 所以直接通过名字找到，然后通过管道使用docker引入 grand代表仓库名，newNSFW代表tag名，根据喜好设定。

### 使用docker安装caffe

在open_nsfw 下有这个文件https://github.com/yahoo/open_nsfw