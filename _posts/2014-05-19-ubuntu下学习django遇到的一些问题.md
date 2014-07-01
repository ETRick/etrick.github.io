---
title: "ubuntu下学习django遇到的一些问题"
layout: post
comments: yes
---
<img src="http://image.zcool.com.cn/12/35/1254494773906.jpg" width="50%" align="right">
#### 1. ubuntu下django‐admin.py startproject mysite 显示“command not found”的解决办法

答案来自[stackoverflow](http://stackoverflow.com/questions/8250086/command-not-found-django-admin-py)

原话是这样的：
>Actually, if you use Ubuntu, it's just django-admin not django-admin.py.
 
>Resides in /usr/bin 
Probably the same thing on Mac.
You're using a Windows tutorial.
 
>It may also tell you
 
>python manage.py runserver
and that is actually
 
>python ./manage.py runserver__

显而易见，django-admin.py应该换成django-admin.

 

 

#### 2. ImportError: Settings cannot be imported, because environment variable DJANGO_SETTINGS_MODULE is undefined. 

请参考《django_中文教程》，原文如下：

创建模板对象
创建一个 Template 对象最简单的方法就是直接实例化它。 Template 类就在 django.template 模块中,构造函
数接受一个参数,原始模板代码。 让我们深入挖掘一下 Python的解释器看看它是怎么工作的。
转到project目录(在第二章由 `django‐admin.py startproject` 命令创建), 输入命令
`python manage.py shell` 启动交互界面。
一个特殊的Python提示符
如果你曾经使用过Python,你一定好奇,为什么我们运行`python manage.py shell`而不是`python`。这两个命令
都会启动交互解释器,但是`manage.py shell`命令有一个重要的不同: 在启动解释器之前,它告诉Django使用
哪个设置文件。 Django框架的大部分子系统,包括模板系统,都依赖于配置文件;如果Django不知道使用哪
个配置文件,这些系统将不能工作。

如果你想知道,这里将向你解释它背后是如何工作的。 Django搜索DJANGO_SETTINGS_MODULE环境变
量,它被设置在settings.py中。例如,假设mysite在你的Python搜索路径中,那么
DJANGO_SETTINGS_MODULE应该被设置为:` mysite.settings `。
当你运行命令:`python manage.py shell`,它将自动帮你处理DJANGO_SETTINGS_MODULE。 在当前的这
些示例中,我们鼓励你使用`python manage.py shell`这个方法,这样可以免去你大费周章地去配置那些你
不熟悉的环境变量。
随着你越来越熟悉Django,你可能会偏向于废弃使用`manage.py shell` ,而是在你的配置文
件.bash_profile中手动添加 DJANGO_SETTINGS_MODULE这个环境变量。


