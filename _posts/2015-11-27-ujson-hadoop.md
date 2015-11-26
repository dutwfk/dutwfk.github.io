---
layout: post
title: 使用ujson优化hadoop的mrjob框架的序列化机制
category: 技术
tags: hadoop，mrjob，ujson
keyword: Hadoop, ujson, 序列化
---

#### 故事的开始

第一次正式在hadoop集群上面跑数据时，遇到一个好玩的事情：

同事小王在看完的代码后，热情的给我添加了下面一段代码，

{% highlight python %}
# -*- coding:utf-8 -*-
import ujson as json
from mrjob.job import MRJob


class UJSONProtocol(object):
    
    def read(self, line):
        raw_key, raw_value = line.split('\t', 1)
        return (raw_key, json.loads(raw_value))
        
    def write(self, key, value):
        return '%s\t%s' % (key, json.dumps(value))
        
        
class UJSONValueProtocol(object):
    
    def read(self, line):
        try:
            return (None, json.loads(line))
        except (ValueError, KeyError, TypeError), e:
            sys.stderr.write(line)
    
    def write(self, _, value):
        return json.dumps(value)
        
        
class ContactsMR(MRJob):

    INTERNAL_PROTOCOL = UJSONProtocol
    OUTPUT_PROTOCOL = UJSONProtocol
    
    def mapper(self, _, line):
        id, contacts = line.split(',')
        contacts = contacts.strip()
        contacts = contacts.split('|')
        for contact in contacts:
            yield contact, 1
            
    def combiner(self, contact, values):
        yield contact, sum(values)

    def reducer(self, contact, counts):
        yield contact, sum(counts)
        
{% endhighlight %}

然后用修改前后的脚本分别跑了一下数据，结果是加了代码后计算时间缩短为原来的三分之一。这几行代码的作用是什么呢？


#### MRJob
mrjob是一个开放源码的Python框架，封装Hadoop的数据流，并积极开发Yelp的。由于Yelp的运作完全在亚马逊网络服务，mrjob的整合与EMR是令人难以置信的光滑和容易（使用 boto包）。

mrjob提供了一个Python的API与Hadoop的数据流，并允许用户使用任何对象作为键和映射器。默认情况下，这些对象被序列化为JSON对象的内部，但也有支持pickle的对象。有没有其他的二进制I / O格式的开箱即用，但有一个机制来实现自定义序列化。

自定义序列化就用到了下面的ujson...

#### UltraJSON

一个号称python中最好的json解析模块UltraJSON，在赖勇浩的blog中有一篇翻译的文章[《UltraJSON——Python 的极速 JSON 编解码器》](http://blog.csdn.net/gzlaiyonghao/article/details/6567408)，这篇文章是ujson作者写的。

ujson的Github地址：[https://github.com/esnme/ultrajson](https://github.com/esnme/ultrajson)

安装：pip install usjon

源码是用c写的，还需在深入研究此间门道...