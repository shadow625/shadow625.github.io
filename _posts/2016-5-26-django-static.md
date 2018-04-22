---
layout:     post
title:      Django static 配置
date:       2016-05-26 12:32:18
categories: Django
---

今天通过网页实现了一个数据库添加员工并显示出来，现在来总结一下遇到的问题。

### 一 static文件添加

以前对于django了解较浅，练习做的网页都是直接将CSS写在HTML文件里面，有不少局限性，真的到实现一个大型网页的时候，这个HTML会变得庞大而不可整理，易读性太差。所以有了需求，就会出来解决方案，django提供static文件机制。通过static机制可以使得模板从服务器的其他（特定）目录寻找CSS、js、image等文件，帮助提升页面的观赏性和功能性。  
  废话不多说，开始介绍这个目录树如图：
![picture](/image/django_static.png)

可以发现在根目录下有一个与你不一样的文件夹——static文件夹，用于放置你的静态文件（CSS JS Image可以看到static下存在对应的三个文件夹），而他们在各个template中被使用，通过相对路径定位到某一静态文件就可以在HTML中添加这一文件。  
要达到这个功能需要进行一些设定，也就是说，告诉django Server 你的static文件夹放在了哪里。

#### 1. 在settings 中添加static配置。

   <pre><code>STATIC_ROOT=os.path.join(BASE_DIR,'static')#指定静态文件的根目录，即就是你的static文件夹的绝对路径。BASE_DIR 是django项目的路径。  
   STATICFILES_DIRS = (
   ```
   ("css", os.path.join(STATIC_ROOT,'css')),
   ("js", os.path.join(STATIC_ROOT,'js')),
   ("images", os.path.join(STATIC_ROOT,'images')),)#生成相应文件夹的路径，以方便直接读取。
   ```
   STATIC_URL = '/static/' 

   </code></pre>

#### 2. 在urls.py 文件中设置。  
   － 需要在url_patterns中添加多余一项  
   － 必须先引入settings 上下文，否则会报错。  
   － url(r'^static/(?P<path>.*)$', 'django.views.static.serve',{ 'document_root':settings.STATIC_ROOT }),

#### 3. 在template中引用外部静态文件。
<pre><code class="HTML">link rel="stylesheet" href="../static/css/slider.css"></link>
</code></pre>

   这基本就是所有需要的设置了。

   ​

   ​





