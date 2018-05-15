---
layout: post
title: spring security
categories: [spring, security]
description: how to perform a security web
keywords: spring security
---

## spring security
首先本文的理解主要源自[spring security](https://docs.spring.io/spring-security/site/docs/5.0.5.RELEASE/reference/htmlsingle/) 的官方文档以及[源代码](https://github.com/spring-projects/spring-security)（里面的注释），部分配置内容来自博客搜索。

本文主要介绍使用spring security 对网站进行安全加固

对于我们的DAO的认证模型，
对于网站的登录一般存在两个步骤，首先是认证，确保此用户为合法的用户，比如密码是否正确，账户是否过期，再者就是授权，表示将赋予这个用户怎样的访问权限，一般由角色定义，比如admin用户登录就能访问后台页面，而user用户登录只能访问web服务器提供的部分服务。这就是authentication 和 authorization，（AAA模型中还会有一个accounting计费）

根据上面所说，我们能够得到我们的需求，首先我们需要有用户表，用来存储认证信息，其中最主要的就是用户名密码。当我们知道这个用户的认证信息无误后，就需要对他进行授权，所以需要对他授予权限，这个权限可以放在用户表项的后面，或者构建较为完善的表结构（USER，ROLE，USER_ROLE）。数据库不是本文的重点，所以一切从简。

我们使用spring data jpa 进行数据库操作，首先需要Entity类，即User ，@Entity 注解声明User类为一个实体类，@Table指定了该实体类绑定于某张表上，因为在application.properties中已经定义了数据源的详细信息，数据库的连接方式，默认的scheme。而此处我们使用lombok插件，使得只需要一个@Data注解就能在编译时帮我们自动加上**getter setter** 和**toString**方法，虽然没节省代码量，但是让工具做，节省了我们很多时间，一个注解比你按出来idea的快捷键并选择生成那些方法要快很多，而且更改变量名的影响也更小。

	@Data
	@Entity
	@Table(name = "t_user")
	public class User 
	{
	    @Id
	    @GeneratedValue
	    private Integer id;
	    private String username;
	    private String password;
	    private Date create_time;
	}

下一步是查找表信息，spring data jpa 有通用的接口，通过repository调用下层ORM模型提供的jpa接口，之前的ORM模型，例如hibernate mybatis openjpa 等虽然都实现了相应的jpa规范，但是不同的模型需要使用不同的使用规范，因此产生各种不同的配置代码，且需要更换模型时需要对源代码进行大量重构，而spring data jpa的作用就是简化这些操作，通过repository统一作为数据源的访问节点，然后再乡下寻找配置的ORM模型，例如hibernate（spring 默认）简化了一直以来被诟病的数据层模板代码冗余的情况

此处只需要做如下的接口继承就能实现数据库的CRUD操作。CrudRepository 定义了一些统一的接口，用于快速调用，如findALL save，等等，我们可以根据我们的需求结合User类中的属性进行自定义查找，而这些只需要声明一个方法，根据方法名你就能知道你要做什么吧，通过用户名查找，那么机器现在也知道了，不用多做什么DAO sql-query 这就够了，方法返回一个可以为null的Optional对象，我们只需要在认证时访问以下这个对象就可以了。

	public interface UserRepository extends CrudRepository<User, Id> {
	    Optional<User> findByUsername(String username);
	}
