---
layout:       post
title:        "Python-迭代器(iterator)、可迭代的(iterable)、生成器(generator)"
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
可以如下实现一个容器（即实现**__contains__** 方法）:'
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
但这个容器类不能通过for循环输出该容器对象的所有元素,即下面代码不能执行
```python
for e in A:
   print(e)
```
执行该代码，显示的错误为
```
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-4-28f7391429f9> in <module>()
----> 1 for e in A:
      2    print(e)

TypeError: 'type' object is not iterable
```
表示这不是一个**可迭代（iterable）**的对象,要使得该容器对象能迭代，必须实现一个**__iter__** 方法 并通过这个方法返回一个**迭代器**对象 。

## 可迭代的

是一个可通过**__iter__** 方法返回一个**迭代器** 对象的类。该类的对象称为"**可迭代对象**"。

对于一个可迭代对象,可以使用 for 来循环遍历其中的元素。比如常见的 list、set和dict。可以用以下isinstance方法来测试对象是否是可迭代（Iterable）

```python
from collections import Iterable
print( isinstance('abc', Iterable)  )    # str是否可迭代
print( isinstance([1,2,3], Iterable) )   # list是否可迭代
print( isinstance(123, Iterable) )       # 整数是否可迭代
```
输出：
```
True
True
False
```

## 迭代器

实现了**__iter__** 和**__next__** 方法的类。 例如下面定义了名为B的**迭代器**类。
```python
class B(object):
    """这个类是个迭代器，因为实现了__iter__和next方法"""
    def __init__(self, n):
        self.idx = 0
        self.n = n
    def __iter__(self):
        return self
    def __next__(self):
        if self.idx < self.n:
            val = self.idx
            self.idx += 1
            return val
        else:
            raise StopIteration()
```
**迭代器** 类的 **__iter__**  方法都返回自身“return self”。即返回一个“ **可迭代的对象** ”

既然**迭代器**类也包含了 **__iter__**,所以**迭代器**也是一个**可迭代的**，但**可迭代的**不一定是迭代器

例如下面的A是一个**可迭代的** 类，通过**__iter__** 返回了一个**迭代器对象** ”即B类的对象.

```python
class A(object):
    """
    A的实例不是迭代器，因为只A实现了__iter__
    但这个类的实例是一个可迭代对象
    因为__iter__返回了B的实例，也就是返回了一个迭代器，因为B实现了迭代器协议
    返回一个迭代器的对象都被称为可迭代对象
    """
    def __init__(self, n):
        self.n = n
    def __iter__(self):
        return B(self.n)
```
下面代码
```python
b = B(3)        # b是一个迭代器，同时b是一个可迭代对象
for i in b:
    print (i)
    
print (iter(b))  

a = A(3)        # a不是迭代器，但a是可迭代对象，它把迭代细节交给了B，B的实例是迭代器
for i in a:
    print (i)
print (iter(a) )  
```
输出
```
0
1
2
<__main__.B object at 0x00000250BC154208>
0
1
2
<__main__.B object at 0x00000250BC099F98>
```

## 参考：


[Python技术进阶——迭代器、可迭代对象、生成器](http://kaito-kidd.com/2018/04/18/python-advance-iterator-generator/)

[python 黑科技之迭代器、生成器、装饰器](https://www.jianshu.com/p/efaa19594cf4) 

[Python Iterator Tutorial](https://www.datacamp.com/community/tutorials/python-iterator-tutorial)
