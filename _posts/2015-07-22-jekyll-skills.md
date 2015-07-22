---
layout: post
title: Jekyll 技巧汇总
category: 技术
tags: [blog,jekyll]
---

简单记录玩博客时遇到的小问题

#### 代码高亮
Jekyll通过Pygments内建支持了代码高亮，支持超过100种语言。为了使这个机制，你需要安装Pygments，而且pygmentize的可执行文件必须在你path路径中，当你运行Jekyll时，确保以Pygments支持的方式运行。

为了表示一个需要高亮的代码块，你需要：{ % highlight ruby % }

{% highlight ruby %}
def foo
	puts 'foo'
end
{% endhighlight %}

highlight的参数是一个编程语言的标示符，你可以在[Lexers](http://pygments.org/docs/lexers/)上找到你所喜欢的编程语言的正确标示符。

#### 行号 

{ % highlight ruby linenos % }

{% highlight ruby linenos %}
def foo
	puts 'foo'
end
{% endhighlight %}
