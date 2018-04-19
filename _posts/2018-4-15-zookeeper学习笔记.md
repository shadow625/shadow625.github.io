---
layout: post
title: ZooKeeper，动物园的管理员
categories: [分布式, web后台]
description: 分布式应用的基础
keywords: zookeeper, kafka ,同步原语，CAP
---

### 0x00前言
zookeeper主要用于分布式服务集群之间同步原语，客户端可以创建获取节点，并通过watcher将节点变更通知到监视器（这是zookeeper的对外主要功能）

### 0x01重要知识点收录
zookeeper 主要有独立模式和主从模式，我们在初期测试学习时较多使用独立模式，而现实中使用基本为主从模式以保证服务的可靠性，可用性。

Znode: zookeeper 使用Znode存储所有元数据，主要是个树形接口，通过类似文件系统的api进行取用，如根节点从`/`开始。

zxid，version：某一节点使用version进行一致性确认，version是一个跟随znode存在的自增的数值，
通过使用版本号并行操作的一致性。

**zookeeper Atomic Broadcast**
>At the heart of ZooKeeper is an atomic messaging system that keeps all of the servers in sync.

如上来自zookeeper官网，zookeeper的核心功能在于实现一个保证一致性的原子消息系统，所以就到了我们介绍一下这个系统运作方式的时候了。<br>
其实就是依赖上述的ZAB协议，进行崩溃恢复的原子广播。正常情况下，客户端会自动连接到集群中任意一台服务器，而写操作会使得这一服务器产生一个事务（*因为zookeeper要保证数据的一致性，即所有客户端访问对任意服务器的访问都是唯一的拷贝，所以当前更改需要通过leader传播给所有follower*），提交事务给leader后，leader需要将其作为proposal广播，通知所有集群同步（*至少是希望能让所有集群马上同步，但是如果等到所有的服务器都同步完成再提供这个数据的访问，会增加很多耗时，收益并不高。所以会取中庸的数值，法定人数，即通过一个法案所需的最少人数，一半以上的投票人*）等到法定数的节点发送tcp的ack报文，即认为此事务可以被接纳，commit 通知所有服务节点更新。

集群中的每个节点会有四个状态**following, leading, electing/looking, observing** 。 其中observe状态为观察者模式，此模式的节点没有写操作的能力，即不对其他节点的信息一致性产生影响，所以不参与ZAB协议中



会话：not connected, connecting, connected, closed ?(closed 和 not connected)

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
