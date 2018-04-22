---
layout: post
title:  django_road-session
categories: django
date:   2015-12-17 12:12:12
---

## django笔记
http 建模 ：描述django响应过程。

1. web服务器收到一个http请求（Apache 收到一个Post请求，通过什么传给django）
2. Django 把web服务器传过来的请求转换成一个请求对象。（django将请求转换成request对象）
3. Django 在 URLconf 里查找正确的视图函数（生成的request对象<中间包括Post/Get消息>传入对应的view文件里的view函数  如home，index ）
4. 调用这个视图函数，参数为请求对象以及任何捕捉到的url 参数（这个视图函数将request进行解析，响应，在这一步进行的有，响应POST消息，查询数据库，并进行返回，动态生成网页：将中间的变量进行填充，渲染返回一个完整的HTML页面，）
5. 然后试图会创建并返回一个响应对象
6. django讲这个响应对象转换成web服务器可以理解的格式
7. web服务器将响应发送给客户端。（返回相应的html网页给客户端）
这个时候：我们有一个问题，如果希望实现登录功能怎么办，django是否提供该功能。
>事实证明django非常强大，回忆起来当时新建app的时候sync 数据库产生了好几个user group 数据库表，现在才知道，django 将用户与app绑定，进行权限控制，每一个没有经过登录认证的用户被视为anonymous user，可以为每一个用户赋予权限。
这时候你肯定也产生了另一个疑问，登录认证怎么办，cookie和session应该怎么处理，
