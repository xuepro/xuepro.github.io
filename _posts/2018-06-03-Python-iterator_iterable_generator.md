---
layout:       post
title:        "Python-迭代器(iterator)、可迭代对象(iterable)、生成器(generator)"
subtitle:     "iterator,iterable,generator"
date:         2018-06-03 17:47:00
author:       "xuepro"
header-img:   "img/home_bg.jpg"
header-mask:  0.3
catalog:      true
multilingual: true
tags:
    - AI
    
---

容器（container）、可迭代对象（iterable）、迭代器（iterator）、生成器（generator）的关系如下图：

![](http://kaito-blog.qiniudn.com/relationships.png?imageMogr2/thumbnail/!70p)

- list、set、tuple、dict都是容器
- 容器通常是一个可迭代对象
- 但凡可以返回一个迭代器的对象，都称之为可迭代对象
- 迭代器是一个可迭代对象，但反之不一定

- 实现了迭代器协议方法的称作一个迭代器
- 生成器是一种特殊的迭代器

## 容器

是存储多个值（对象）的数据类型，如list,tuple,set,dict等都是容器，容器是实现了**__contains__** 方法的类，从而可以用in或not in语法得知某个元素是否在容器内。

```python
print (1 in [1, 2, 3])             # True
print (2 not in (1, 2, 3) )        # False
print ('a' in ('a', 'b', 'c') )    # True
print ('x' in 'xyz' )              # True
print ('a' not in 'xyz')           # True
```
```
True
False
True
True
True
```
可以如下顶一个一个容器（即实现**__contains__** 方法）:'
```python
class A(object):
    def __init__(self):
        self.items = [1, 2]
    def __contains__(self, item):   # x in y
        return item in self.items
    
    
a = A()
print (1 in a )   # True
print (2 in a )  # True
print (3 in a )   # False
```



参考：
[Python技术进阶——迭代器、可迭代对象、生成器](http://kaito-kidd.com/2018/04/18/python-advance-iterator-generator/)

[python 黑科技之迭代器、生成器、装饰器](https://www.jianshu.com/p/efaa19594cf4) 
