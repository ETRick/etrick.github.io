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


##django一些笔记

#####6-26

- 用到template的时候 使用命令python manage.py shell而不是python：manage.py shell命令有一个重要的不同： 在启动解释器之前，它告诉Django使用哪个设置文件。 Django框架的大部分子系统，包括模板系统，都依赖于配置文件；如果Django不知道使用哪个配置文件，这些系统将不能工作。

- t.render(c)返回的值是一个Unicode对象，不是普通的Python字符串

- 使用到{{ name }} ,{{var.upper}}, {% if ordered_warrenty%}

- 用字典传递（template)

- 对于template中传递的列表不允许使用负数列表索引. {{ items.-1 }} 这样的模板变量将会引发`` TemplateSyntaxError``，应该是items.2

- ######当模板系统在变量名中遇到点时，按照以下顺序尝试进行查找（短路逻辑。）：
    - 字典类型查找 （比如 foo["bar"] )
    - 属性查找 (比如 foo.bar )
    - 方法调用 （比如 foo.bar() )
    - 列表类型索引查找 (比如 foo[bar] )


- `silent_variable_failure` 属性并且值为 True ，方法异常就不会传递

- `alters_data` 函数属性（模板系统不会执行任何以该方式进行标记的方法）

- 如何处理无效变量:展示为空字符串

- 也可以使用标准的Python字典语法(syntax)向``上下文(Context)`` 对象添加或者删除条目

- ###基本的模板标签和过滤器
	- {% if %} 和 {% endif %} 
	- 空或Fasle的东西都表示布尔值的False，除此都为True
	- {% if %} 标签不允许在同一个标签中同时使用 and 和 or
	- 没有 {% elif %} 标签
	- {%for ...reversed %},反向迭代
	- 在执行循环之前先检测列表的大小是一个通常的做法，当列表为空时输出一些特别的提示。所以`` for`` 标签支持一个可选的`` {% empty %}`` 分句，通过它我们可以定义当列表为空时的输出内容 下面的例子与之前那个等价
	- `` forloop`` 的模板变量。这个变量有一些提示循环进度信息的属性。，
	- forloop.counter，意如其名，初次设置为1
	- forloop.counter0 则从0开始计数
	- forloop.revcounter 是表示循环中剩余项的整型变量
	- forloop.revcounter0 
	- forloop.first 是一个布尔值

- Django模板系统压根儿就没想过实现一个全功能的编程语言，所以它不允许我们在模板中执行Python的语句

- {% ifequal %} 和 {% endifequal %}， 支持可选的 {% else%} 标签

- 只有模板变量，字符串，整数和小数可以作为 {% ifequal %} 标签的参数

- 注释{# This is a comment #}，多行注释{% comment %}

- 模板过滤器是在变量被显示前修改它的值的一个简单方法

- 过滤器的参数跟随冒号之后并且总是以双引号包含

- 1.6以后版本已经不需要这么做了。不需要寻找模板路径。可以添加`TEMPLATE_DIRS=( os.path.join(BASE_DIR,'templates'),)`

- Python 要求单元素元组中必须使用逗号

- 位于 django.shortcuts 模块中名为 render_to_response() ,简化代码（一次性载入某个模板文件，第一个参数是模板，第二个是字典）

- locals() **返回**的**字典**对所有__局部__变量的名称与值进行映射,注意这时候的字典键得注意要与模板中的相同。

- include 模板标签：允许在模板中包含其他模板内容。

- 所有的 {% block %} 标签告诉模板引擎，子模板可以重载这些部分