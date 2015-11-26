---
layout: post
title: 实用的LinuxShell命令们
category: 整理
tags: config 
keyword: vim,配置
---
> 整理工作中遇到的使用Linux Shell命令们

##### kill 一个服务启动的多个进程：

{% highlight sh %}
ps -ef | grep xxx | grep -v grep | cut -c 9-15 | xargs kill -9
{% endhighlight %}

- ps - ef: 是Red Hat 里查看所有进程的命令；
- grep xxx: 的输出结果是，所有含有关键字“xxx”的进程；
- grep -v grep: 是在列出的进程中去除含有关键字“grep”的进程；
- cut -c 9-15: 是截取输入行的第9个字符到第15个字符，而这正好是进程号PID；
- xargs kill -9: 中的xargs命令是用来把前面命令的输出结果（PID）作为“kill -9”命令的参数，并执行该令；