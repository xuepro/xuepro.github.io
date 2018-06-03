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

文章来源：[Python技术进阶——迭代器、可迭代对象、生成器](http://kaito-kidd.com/2018/04/18/python-advance-iterator-generator/)

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
即A类的**__iter__** 返回的**迭代器对象**是B类的对象。因此，B类对象既是迭代器对象又是可迭代对象，而A类对象仅仅是可迭代对象而不是迭代器对象。

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
上述的for循环中就是调用**next** 函数得到迭代器对象（即将迭代器对象传给**next** 函数）的下一个值的。

可以调用*next* 函数作用于一个迭代器对象，得到该迭代器对象中的下一数据元素的值，但不能将*next* 函数作用于一个可迭代对象。



```python
b = B(5)
a = A(5)
print(next(b))
print(next(a))
```
输出为
```
---------------------------------------------------------------------------
TypeError                                 Traceback (most recent call last)
<ipython-input-23-44d8a918ee80> in <module>()
      2 a = A(5)
      3 print(next(b))
----> 4 print(next(a))

TypeError: 'A' object is not an iterator
```

我们熟悉的内置类型对象list、tuple、set、dict，都是可迭代对象，但不是一个迭代器，因为其内部都把迭代细节交给了另外一个类，这个类才是真正的迭代器：

## 生成器
生成器是特殊的迭代器，它也是个可迭代对象。

有2种方式可以创建一个生成器：

- 生成器表达式
- 生成器函数

### 生成器表达式 

    类似于 列表表达式(综合式)，即将 列表表达式的```[]``换成了```()```。例如
    
```python
g = (i for i in range(5))   # 创建一个生成器
print(g)
it = iter(g)         # 生成器就是一个迭代器
print(it)
```

输出

```
<generator object <genexpr> at 0x00000250BC1049E8>
<generator object <genexpr> at 0x00000250BC1049E8>
```

生成器也是一个可迭代对象,当然可以用for遍历它

```python
for i in g:     # 生成器也是一个可迭代对象
   print (i)
```

### 生成器函数: 

包含yield关键字的函数.

```python
# 生成器函数
def gen(n):   
    for i in range(n):
        yield i
        
g = gen(5)        # 创建一个生成器
print (g)           
print ( type(g) )   # <type 'generator'>

# 迭代
for i in g:
    print (i)    
```

输出
```
<generator object gen at 0x00000250BC142728>
<class 'generator'>
0
1
2
3
4
```

这个函数与包含return的函数执行机制不同：

- 包含return的方法会以return关键字为终结返回，每次执行都返回相同的结果
- 包含yield的方法一般用于迭代，每次执行遇到yield即返回yield后的结果，但内部会保留上次执行的状态，下次迭代继续执行yield之后的代码，直到再次遇到yield并返回

当我们想得到一个很大的集合时，如果使用普通方法，一次性生成出这个集合，然后return返回：

```python
def gen_data(n):
    return [i for i in range(n)]    # 一次性生成大集合
```

但如果这个集合非常大时，就需要在内存中一次性占用非常大的内存。

使用yield能够完美解决这类问题，因为yield是懒惰执行的，一次只会返回一个值：

```python
def gen_data(n):
    for i in range(n):
        yield i         # 每次只生成一个元素 
```
然后，这样使用它

```python
for e in gen_data(8):
    print(e) 
```

输出为：
```
0
1
2
3
4
5
6
```

再如，我们可以写出斐波拉契数列的生成器函数
```python
def fib(max):
    n, a, b = 0, 0, 1
    while n < max:
        yield b
        a, b = b, a + b
        n = n + 1
    return 'done'
```

然后这样使用

```python
for a in fib(8):
    print(a) 
```

输出为

```
1
1
2
3
5
8
13
21
```

## 参考：




[python 黑科技之迭代器、生成器、装饰器](https://www.jianshu.com/p/efaa19594cf4) 

[Python Iterator Tutorial](https://www.datacamp.com/community/tutorials/python-iterator-tutorial)
