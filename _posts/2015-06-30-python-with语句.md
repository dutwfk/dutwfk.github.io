---
layout: post
title: Python With语句
category: 技术
tags: [Python]
---

with 语句是从 Python 2.5 开始引入的一种与异常处理相关的功能（2.5 版本中要通过 from __future__ import with_statement 导入后才可以使用），从 2.6 版本开始缺省可用（参考 What's new in Python 2.6? 中 with 语句相关部分介绍）。

with 语句适用于对资源进行访问的场合，确保不管使用过程中是否发生异常都会执行必要的“清理”操作，释放资源，比如文件使用后自动关闭、线程中锁的自动获取和释放等。


## 类型判断

### instance

* isinstance(eval("123"), int)
* isinstance(eval("123.23"), float)

### type

### 内置

* s.isalnum()  所有字符都是数字或者字母s.isalpha()  所有字符都是字母s.isdigit()  所有字符都是数字
* s.islower()  所有字符都是小写s.isupper()  所有字符都是大写s.istitle()  所有单词都是首字母大写，像标题
* s.isspace()  所有字符都是空白字符、\t、\n、\r
* if ’name’ in dict_ret.keys():

### 修饰器

作用：

### HTTP
