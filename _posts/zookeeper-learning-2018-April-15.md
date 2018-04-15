---
layout: post
title: ZooKeeper，动物园的管理员
categories: [分布式, web后台]
description: 分布式应用的基础
keywords: zookeeper, kafka ,同步原语，CAP
---

### 0x00前言
zookeeper 很强

### 0x01重要知识点收录
Znode
通知模式进行数据处理，
通过使用版本号阻止并行操作的一致性。
会话：not connected connecting connected,closed ?(closed 和 not connected)

		dataDir=/Users/shadow/prog/java_develop/spring/configkafka/z2
		clientPort=2181
		tickTime=2000
		initLimit=10
		syncLimit=5

		server.1=192.168.1.105:3333:3334
		server.2=192.168.1.103:3333:3334
		server.3=192.168.1.103:5555:5556
<br>

- dataDir：随意指定一个位置，用于存放配置数据等。
- tickTime 心跳时间
- initLimit 这是在初始化时选举所需要的时间，以心跳的倍数计算，即10*tickTime
- syncLimit leader 和 follower 之间同步消息的间隔
- config中存在三个服务器的地址和端口号，后面的两个端口号分别为仲裁通信和群首选举。开启zk服务时需要制定配置文件，然后zk会根据配置文件中dataDir位置找到dataDir下的myid数据，用来标识自己在这三个服务器中的位置。		
