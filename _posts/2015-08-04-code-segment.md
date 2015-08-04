---
layout: post
title: [摘] 代码片段
category: 技术
tags: [code]
---
string.maketrans设置字符串转换规则表(translation table)

    allchars = string.maketrans('', '')  #所有的字符串，即不替换字符串
    aTob = string.maketrans('a','b')  #将字符a转换为字符b
    
---    
translate函数进行字符串的替换和删除，第一个参数是字符串转换规则表(translation table)，第二个参数是要删除的字符串。比如，要将字符串s中的所有e替换为a，同时要删除所有的o


    aTob = string.maketrans('e','a')
    s = 'hello python'
    print s.translate(aTob, 'o')

---
    import string
    def translator(frm='', to='', delete='', keep=None):
       if len(to) == 1:
           to = to * len(frm)
       trans = string.maketrans(frm, to)
       if keep is not None:
           allchars = string.maketrans('', '')
           delete = allchars.translate(allchars, keep.translate(allchars, delete))
       def translate(s):
           return s.translate(trans, delete)
       return translate
       
调用：

    digits_only = translator(keep=string.digits)
    print digits_only('Chris Perkins : 224-7992')
    
    digits_to_hash = translator(frm=string.digits, to='#')
    print digits_to_hash('Chris Perkins : 224-7992')

    result：
        2247992
        Chris Perkins : ###-####

---
大小写转换

    s = 'hEllo pYthon'
    print s.upper()
    print s.lower()
    print s.capitalize()
    print s.title()
    
---

条件判断

    print (1==2) and 'Fool' or 'Not bad'
    result：Not bad
    
---
遍历数组

    for index, item in enumerate(sequence):
        process(index, item)
        
---
Copy对象：深拷贝和浅拷贝

    import copy
    a = [1, 2, 3, 4, ['a', 'b']]  #原始对象
    
    b = a  #赋值，传对象的引用
    c = copy.copy(a)  #对象拷贝，浅拷贝，此时：拷贝子对象的引用
    d = copy.deepcopy(a)  #对象拷贝，深拷贝
    
    a.append(5)  #修改对象a
    a[4].append('c')  #修改对象a中的['a', 'b']数组对象
    
    print 'a = ', a
    print 'b = ', b
    print 'c = ', c
    print 'd = ', d
    
---

Map函数

    import os

    def anyTrue(predicate, sequence):
        return True in map(predicate, sequence)
    
    def filterFiles(folder, exts):
        for fileName in os.listdir(folder):
            if os.path.isdir(folder + '/' + fileName):
                filterFiles(folder + '/' + fileName, exts)
            elif anyTrue(fileName.endswith, exts):
                print fileName
    
    exts = ['.rmvb', '.avi', '.pmp']
    filterFiles('/media/Personal/Movie', exts)
    
CookBook一书中，提供的是itertools.imap来实现对字符串的过滤。imap和map不同的是，imap返回的是一个iteration对象，而map返回的是一个list对象。代码如下:

    import itertools
    def anyTrue(predicate, sequence):
        return True in itertools.imap(predicate, sequence)
    def endsWith(s, *endings):
        return anyTrue(s.endswith, endings)
   
imap 等价于：

    def imap(function, *iterables):
         iterables = map(iter, iterables)
         while True:
             args = [i.next() for i in iterables]
             if function is None:
                 yield tuple(args)
             else:
                 yield function(*args)
                 
