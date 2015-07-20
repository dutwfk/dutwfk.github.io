---
layout: post                                  
title: pip安装MySQL-python包错误解决
category: 技术                                  
tags: [python,mysql]                                   
---

在Mac电脑上和64位Linux系统中的某一python的virtualenv中安装MySQL-python包，会出现错误。

出现的原因是因为新安装的Mysql的库文件路径没有包含在系统的路径内。

解决的办法参考stackoverflow：

- http://stackoverflow.com/questions/5178292/pip-install-mysql-python-fails-with-environmenterror-mysql-config-not-found

```
export PATH=$PATH:/usr/local/mysql/bin

```
- http://stackoverflow.com/questions/4559699/python-mysqldb-and-library-not-loaded-libmysqlclient-16-dylib

```
export DYLD_LIBRARY_PATH=/usr/local/mysql/lib/
```

