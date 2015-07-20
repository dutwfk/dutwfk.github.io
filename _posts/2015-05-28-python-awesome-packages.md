---
layout: post                                  
title: 相见恨晚 python依赖包
category: 技术                                  
tags: [python,packages]    
                               
---
## python依赖包
> 关键字：pip、virtualenv、xx/lib/python2.7/site-packages/

目前常见的一些自动化安装工具，比如pip，easy_install，distribute等，自动帮你下载源码，并安装。

最流行的软件包管理工具pip：

常用命令:

* 从PyPI安装软件包：
	* pip install SomePackage
* 查看软件包安装了哪些文件及路径等信息：
	* pip show --files SomePackage
* 查看哪些软件包已经有更新版本：
	* pip list --outdated
* 升级软件包：
	* pip install --upgrade SomePackage
* 卸载软件包：
	* pip uninstall SomePackage

高级用法:

* 查询软件包
	* pip search "query"
* 列出安装的所有软件包
	* pip list
* 安装软件包的指定版本号
	* pip install SomePackage            # latest version
	* pip install SomePackage==1.0.4     # specific version
	* pip install 'SomePackage>=1.0.4'     # minimum version4 
* 根据依赖文件安装软件包。
	* 创建了一个感觉的虚拟环境，然后安装了一些依赖的软件包，开发出了应用APP。需要部署到服务器的时候可以使用pip导出依赖文件列表，然后在服务器上根据依赖文件列表，自动安装对应的软件包。
	* pip freeze > requirements.txt
	* pip install -r requirements.txt


### web框架:
* django
* flask
* tornado
* web.py
* gevent

### 微信框架：
* WeRoBot


### 网络：
* requests
* httpie


### 爬虫：
* scrapy
* Beautifulsoup


### 系统方面：
* fabric
* ansible


### ORM：
* peewee
* sqlalchemy


### 模板引擎：
* jinja2


### 图像处理：
* Pillow
* Python Imaging Library (PIL)


### 命令行应用：
* docopt

### 静态网站生成器
* pelican


### 数据处理：
* pandas


### 其他：
* awesome-python


### 自动化：
* sh：可以用 Python 函数的语法去调用 shell 命令，sh 之于 subprocess 类似 requests 之于 urllib2。
* Watchdog：监视文件系统改动。
* Path：简化文件系统相关操作。


---

### Django专版
* django-debug-toolbar
* django-rest-framework
* django-xadmin
* wagtail
* pinax
* mezzanine
* django-crispy-forms
* django-compressor
* django-grappelli
* django-taggit
* django-basic-apps
* django-userena
* django-mptt
* sorl-thumbnail
* django-guardian
* django-pipeline