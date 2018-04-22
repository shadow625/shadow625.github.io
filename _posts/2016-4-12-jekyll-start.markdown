---
layout: post
title: jekyll——安装过程及界面定制
categories: FunCode
description: some word here
keywords: keyword1, keyword2
date:   2016-4-15 12:12:12
---



### jekyll background

用jekyll好久了（好吧一直是通过github-page简介用的）今天终于在自己的电脑上搭好了Jekyll的本地环境（你问我装了多长时间： 6个月你信不信）在这里记录下Jekyll的搭建和使用的一些经验吧   

首先我是在github—pages 上第一次接触Jekyll 
当时正想搭建一个博客平台，但是感觉wordpress太low（应该就是了解不深导致印象不好吧），自己写前段改代码又太菜，这时实验室同桌在搞的一个博客界面吸引了我的眼球，界面很清新，功能不多不少，正是我脑海中完美的一个博客环境，（对，没错 我就是那个时候才知道有github-pages这个东西）而且有很多漂亮的开源模板可以使用（不信是吧，来看看[*Jekyll主题*](http://jekyllthemes.org/))   

### 安装Jekyll###
* github主页就是通过Jekyll渲染的，也就是说在他的后台肯定是配备了一个Jekyll环境，我们现在就是试图在本地搭建一个一模一样的环境，用于本地测试。当然你要是一片markdown错误率能保持在0以下，那么这环境就是多余的了。（想想应该不可能呢，因为你还有耐心在看这篇文，说明我们俩水平差不多吧）   
  根据[*Jekyll官网*](https://jekyllrb.com/)给的简单的示例。  
    <pre><code>  $ gem install jekyll
    $ jekyll new my-awesome-site
    $ cd my-awesome-site
    $ jekyll serve</code></pre>   
* 然而事实并没有那么简单在我执行第一步的时候就卡住了，发现Mac是自带Ruby的，我就直接输入命令泡好茶等结果，然后发现他一直执行不出来，然后就开始查（此处省略好多字）
  ![no_response](/image/gem_no_response.png)
  最后知道，需要执行`gem update --system `（什么鬼，感觉就像yum的更新源吧）然后执行Jekyll安装就顺利了。（还是没有反应的话借个梯子试试）
  后面的事情就很轻松了，如果这个时候你在上面选好了你的界面模板，那就git clone过来，在模板根目录下直接`Jekyll serve`就可以在本地访问你的准博客界面了。   
##界面定制##
这个我并不是前端专家，但是模板都有了，做一些改动的话还是很轻松的嘛。
如果你有过django开发经历处理这个就太简单了。他们两个之间的差异很小，上手很容易。现在来介绍一下他的目录结构   

<pre><code calss="html">.
    |── _config.yml
    |── _drafts
    |   |── begin-with-the-crazy-ideas.textile
    |   |── on-simplicity-in-technology.markdown
    |── _includes
    |   |── footer.html
    |   |── header.html
    |── _layouts
    |   |── default.html
    |   |── post.html
    |── _posts
    |   |── 2007-10-29-why-every-programmer-should-play-nethack.textile
    |   |── 2009-04-26-barcamp-boston-4-roundup.textile
    |── _site
    |── .jekyll-metadata
    |── index.html
</code></pre>

### 目录分析

​	根目录下有一个_config.yml 文件 用于存储你的页面的渲染设置，或者你的一些将在全站用到的一些信息条目，例如你的名字，个人网址，以及markdown类型。  
​	然后是_includes 类似于django的模板嵌套，Jekyll支持多个模块拼凑出一个完整的页面，例如在例子中出现的footer.html 将作为页面的最下面的一部分出现，他对于页面的贡献由你决定，为了方便管理与查找，每个人都会养成一个自己的习惯，在header中存放script、CSS等文件引用，footer中存放一些页面内的js脚本。可以抽象的理解为 _include 中的文件都是一个个装饰模块，而外部的index.html就是一个房子的框架，将一个个装饰模块填充在房子的框架上，就能盖成一个完美的房子。   
​	而处于_layout 下的文件顾名思义为布局文件，你希望你的不同类的页面能通过不同的界面显示，而这就由布局文件决定的，通过定义不同的布局文件可以实现上述目的。   
​	下一个post文件夹 就是这个站的主体，你的文章所在的位置了。每一篇文章由markdown书写，Jekyll自带···markdown解释器。

​	这就是整个目录树比较重要的几个部分了。

