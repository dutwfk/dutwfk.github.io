---
layout: post                                   #这个博客的布局文件
title: 社交网站关注粉丝的Redis实践     #博客标题
category: 技术                                  #博客分类
tags: [Redis,sns]                                   #博客标签 
---

实现采用 Redis 存储用户关系

针对类似微博，贴吧，论坛的用户关系设计，目前成熟的设计更多得倾向与Redis。

redis就是一个存储key-value键值对的仓库，如何使用redis在于如何理解你需要设计的系统的E-R的模型，然后合理的规划redis的数据库结构

### 具体案例