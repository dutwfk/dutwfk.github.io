---
layout: page
title: bug_list
image:
  feature: abstract-2.jpg
modified: 2015-07-22
---

bug_list

> pkg_resources.DistributionNotFound: ndg-httpsclient

![](http://7u2n3n.com1.z0.glb.clouddn.com/images/bug_pip_update.png)

-----

> 在Mac电脑上和64位Linux系统中的某一python的virtualenv中安装MySQL-python包，会出现错误。

出现的原因是因为新安装的Mysql的库文件路径没有包含在系统的路径内。

解决的办法参考stackoverflow：

- http://stackoverflow.com/questions/5178292/pip-install-mysql-python-fails-with-environmenterror-mysql-config-not-found

	export PATH=$PATH:/usr/local/mysql/bin

- http://stackoverflow.com/questions/4559699/python-mysqldb-and-library-not-loaded-libmysqlclient-16-dylib

	export DYLD_LIBRARY_PATH=/usr/local/mysql/lib/