---
layout: post                                  
title: pip安装MySQL-python包错误解决
category: 技术                                  
tags: [python,mysql]                                   
---

- http://stackoverflow.com/questions/5178292/pip-install-mysql-python-fails-with-environmenterror-mysql-config-not-found

```
export PATH=$PATH:/usr/local/mysql/bin

```
- http://stackoverflow.com/questions/4559699/python-mysqldb-and-library-not-loaded-libmysqlclient-16-dylib

```
export DYLD_LIBRARY_PATH=/usr/local/mysql/lib/
```