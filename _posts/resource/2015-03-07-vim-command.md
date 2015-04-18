---
layout: post
title: Vim 常用命令
category: 整理
---



### 翻页命令
- Ctrl + B (Backward)：向上翻一页，Ctrl + F (Forward)：向下翻一页
- Ctrl + D (Down)：向下滚半屏，Ctrl + U (Up)：向上滚半屏
- {：以段落为单位，向上翻动
- }：以段落为单位，向下翻动

以上两命令在使用时需要按住Shift键，因为大括号所在的键位还有一个中括号
 
### 窗口分割
* :sp：水平分割
* :vsp：垂直分割
* :diffs：分割出一个文件比较窗口

### 窗口跳转
* 方法一：先按Ctrl + W，然后按相应的方向键，上k、下j、左h、右l
* 方法二：直接按Ctrl + 方向键，如Ctrl + J、Ctrl + L

### 代码补全
* Ctrl + P：可以补全在本次Vim进程中出现过的所有词汇，包括中文。也就是说只要你之前敲过的代码，你就不必要重复劳动了，但只限于本次Vim进程
* Ctrl + N：经测试，此命令只在Linux和Cygwin环境下有效，使用它可以自动搜索C/C++函数库，然后就可以进行C/C++的函数补全了
* 还有支持其他语言的代码补全插件，如Python、jQuery等，这个可以自己去搜寻自己需要的插件，然后按其要求设置或使用快捷键即可

### 删除命令
* x：删除光标当前所在字符
* 3x：连续删除从当前光标起的3个字符
* dw：删除从当前光标到单词结尾的所有字符
* d$：删除当前光标到行尾的所有字符，等价于D
* dG：删除当前光标到文件末尾的所有内容
* d1G：删除从文件开始到当前行的所有内容，包括当前行
* dd：删除当前行
* 3dd：删除从当前行开始的3行
* :10,15d：删除指定范围的内容
 
### 复制命令

* yy：复制当前行，等价于Y
* 3yy：复制从当前行开始的3行

### 粘贴命令
* p(小写)：将缓冲区内容粘贴到当前行的下方
* P(大写)：粘贴到当前行的上方

### 替换命令
* r：替换单个字符
* R：连续替换多个字符
* cw：删除从当前光标到单词结尾的所有字符，并转入插入模式，以便修改
* c$：删除当前光标到行尾的所有字符，并转入插入模式
* :s/old/new/g：针对当前行的替换
* :12,15s/old/new/g：针对指定范围的替换
* :%s/old/new/g：全文替换
 
### 文件相关
* :w：保存文件
* :w abc.txt：另存为新的文件名
* :12,25 w abc.txt：将指定范围的内容保存成一个新的文件
* :r abc.txt：将另一个文件的内容插入当前文档
 
### 定位命令

* gg：转到文件头部
* G：转到文件尾部
* 20G：转到第20行，等价于:20
* H：定位到屏幕上半部分
* M：定位到屏幕中部
* L：定位到屏幕下半部分
 
### 搜索命令

* /关键字：正向查找
* ?关键字：逆向查找
* n：那查找顺序跳转到下一个关键字
* N：反查找顺序跳转到上一个关键字
* %：在括号上按百分号，可以自动跳转到与其匹配的另一半括号，支持小括号、中括号、大括号
 
### 批量注释

Vim的特殊变量：^代表行首，$代表行尾，可以利用替换命令实现批量注释，用反斜杠实现转义

在行首批量添加注释：
* :10,15s/^/\/\//g（针对C/C++）
* :10,15s/^/#/g（针对Perl、Python）
 
批量取消注释：
* :10,15s/^\/\///g（针对C/C++）
* :10,15s/^#//g（针对Perl、Python）
 
##启示小记
* dw、d$和cw、c$基本类似，只是前两者只进行删除，而后两者除了删除还自动转入插入模式
* :sh：暂时退出Vim，进入Shell界面（Windows下是Dos界面），待退出Shell或Dos以后自动返回Vim 
* :r !操作系统命令：可以将其后所接的Shell或Dos命令执行的结果插入当前文档
* 启动时使用vim -r或gvim -r可以查看是否存在交换文件
* 使用vim -r 文件名恢复指定的交换文件
