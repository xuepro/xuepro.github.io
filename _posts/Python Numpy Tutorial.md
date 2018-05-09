
---
layout:       post
title:        "Python numpy 教程"
subtitle:     "Python Numpy Tutorial"
date:         2018-05-08 17:51:00
author:       "xuepro"
header-img:   "img/home_bg.jpg"
header-mask:  0.3
catalog:      true
multilingual: true
tags:
    - Python 
    
---    
## Python Numpy 教程(Python Numpy Tutorial)

这篇教程来自[Justin Johnson](https://cs.stanford.edu/people/jcjohns/)。


我们将使用Python编程语言来完成本课程的所有作业。Python是一门非常好的通用编程语言，凭借一些流行的库（numpy, scipy, matplotlib），成为了一个强大的科学计算环境。

我们期望你们中大多数人对于Python语言和Numpy库有一些经验，对于其他读者，这篇教程可以帮助你们快速了解Python编程语言和用Python进行科学计算。

对于有Matlab的读者，我们推荐阅读[numpy for Matlab users](http://wiki.scipy.org/NumPy_for_Matlab_Users)。

你还可以查看由[Volodymyr Kuleshov](http://web.stanford.edu/~kuleshov/)和[Isaac Caswell](https://symsys.stanford.edu/viewing/symsysaffiliate/21335)为课程[CS 228](http://cs.stanford.edu/~ermon/cs228/index.html)创建的本教程的[IPython notebook](https://github.com/kuleshov/cs228-material/blob/master/tutorials/python/cs228-python-tutorial.ipynb)版本。

内容列表：
 * Python
    * 基本数据类型
    * 容器
       * 列表
       * 字典
       * 集合
       * 元组
    * 函数
    * 类    
 * Numpy
   * 数组
   * 访问数组
   * 数据类型
   * 数组的数学
   * 广播
 * SciPy
   * 图像操作
   * MATLAB文件
   * 点之间的距离
 * Matplotlib
   * 绘制图形
   * 子图
   * 图像
   
 ### Python
   
Python是一种高级的，动态类型的多范型编程语言。很多时候，大家会说Python看起来简直和伪代码一样，这是因为你能够通过很少行数的代码表达出很有力的思想。举个例子，下面是用Python实现的经典的quicksort算法例子：

```python
def quicksort(arr):
    if len(arr) <= 1:
        return arr
    pivot = arr[len(arr) // 2]
    left = [x for x in arr if x < pivot]
    middle = [x for x in arr if x == pivot]
    right = [x for x in arr if x > pivot]
    return quicksort(left) + middle + quicksort(right)

print(quicksort([3,6,8,10,1,2,1]))
# Prints "[1, 1, 2, 3, 6, 8, 10]"
```

### Python版本

Python有两个支持的版本，分别是2.7和3.4。这有点让人迷惑，3.0向语言中引入了很多不向后兼容的变化，2.7下的代码有时候在3.4下是行不通的。在这个课程中，我们使用的是2.7版本。

如何查看版本呢？使用python --version命令。
```
>>>python --version
python 2.7.11
```

### 基本数据类型

和大多数编程语言一样，Python拥有一系列的基本数据类型，比如整型、浮点型、布尔型和字符串等。这些类型的使用方式和在其他语言中的使用方式是类似的。

**数字(Numbers)**：整型和浮点型的使用与其他语言类似。

```python
x = 3
print(type(x)) # Prints "<class 'int'>"
print(x)       # Prints "3"
print(x + 1)   # Addition; prints "4"
print(x - 1)   # Subtraction; prints "2"
print(x * 2)   # Multiplication; prints "6"
print(x ** 2)  # Exponentiation; prints "9"
x += 1
print(x)  # Prints "4"
x *= 2
print(x)  # Prints "8"
y = 2.5
print(type(y)) # Prints "<class 'float'>"
print(y, y + 1, y * 2, y ** 2) # Prints "2.5 3.5 5.0 6.25"
```

需要注意的是，Python中没有 x++ 和 x-- 的操作符。

Python也有内置的长整型和复杂数字类型，具体细节可以查看文档。

**布尔型(Booleans)** ： Python实现了所有的布尔逻辑，但用的是英语，而不是我们习惯的操作符（比如&&和||等）。

```python
t = True
f = False
print(type(t)) # Prints "<class 'bool'>"
print(t and f) # Logical AND; prints "False"
print(t or f)  # Logical OR; prints "True"
print(not t)   # Logical NOT; prints "False"
print(t != f)  # Logical XOR; prints "True"
```

**字符串(Strings)** ：Python对字符串的支持非常棒。

```python
hello = 'hello'    # String literals can use single quotes
world = "world"    # or double quotes; it does not matter.
print(hello)       # Prints "hello"
print(len(hello))  # String length; prints "5"
hw = hello + ' ' + world  # String concatenation
print(hw)  # prints "hello world"
hw12 = '%s %s %d' % (hello, world, 12)  # sprintf style string formatting
print(hw12)  # prints "hello world 12"
```
字符串对象有一系列有用的方法，比如：

```python
s = "hello"
print(s.capitalize())  # Capitalize a string; prints "Hello"
print(s.upper())       # Convert a string to uppercase; prints "HELLO"
print(s.rjust(7))      # Right-justify a string, padding with spaces; prints "  hello"
print(s.center(7))     # Center a string, padding with spaces; prints " hello "
print(s.replace('l', '(ell)'))  # Replace all instances of one substring with another;
                                # prints "he(ell)(ell)o"
print('  world '.strip())  # Strip leading and trailing whitespace; prints "world"
```

如果想详细查看字符串方法，请看[文档](https://docs.python.org/3.5/library/stdtypes.html#string-methods)。

### 容器(Containers)

Python包含一些内在容器类型：列表（lists）、字典（dictionaries）、集合（sets）和元组（tuples）。

**列表（Lists）**
列表就是Python中的数组，但是列表长度可变，且能包含不同类型元素。
```python
xs = [3, 1, 2]    # Create a list
print(xs, xs[2])  # Prints "[3, 1, 2] 2"
print(xs[-1])     # Negative indices count from the end of the list; prints "2"
xs[2] = 'foo'     # Lists can contain elements of different types
print(xs)         # Prints "[3, 1, 'foo']"
xs.append('bar')  # Add a new element to the end of the list
print(xs)         # Prints "[3, 1, 'foo', 'bar']"
x = xs.pop()      # Remove and return the last element of the list
print(x, xs)      # Prints "bar [3, 1, 'foo']"
```

列表的细节，同样可以查阅[文档](https://docs.python.org/3.5/tutorial/datastructures.html#more-on-lists)。


**切片(Slicing)** ：为了一次性地获取列表中的元素，Python提供了一种简洁的语法，这就是切片。

```python
nums = list(range(5))     # range is a built-in function that creates a list of integers
print(nums)               # Prints "[0, 1, 2, 3, 4]"
print(nums[2:4])          # Get a slice from index 2 to 4 (exclusive); prints "[2, 3]"
print(nums[2:])           # Get a slice from index 2 to the end; prints "[2, 3, 4]"
print(nums[:2])           # Get a slice from the start to index 2 (exclusive); prints "[0, 1]"
print(nums[:])            # Get a slice of the whole list; prints "[0, 1, 2, 3, 4]"
print(nums[:-1])          # Slice indices can be negative; prints "[0, 1, 2, 3]"
nums[2:4] = [8, 9]        # Assign a new sublist to a slice
print(nums)               # Prints "[0, 1, 8, 9, 4]"
```

我们将在Numpy数组部分再次看到切片。


**循环(Loops)** ：我们可以这样遍历列表中的每一个元素：

```python
animals = ['cat', 'dog', 'monkey']
for animal in animals:
    print(animal)
# Prints "cat", "dog", "monkey", each on its own line.
```

如果想要在循环体内访问每个元素的索引，可以使用内置的enumerate函数
```python
animals = ['cat', 'dog', 'monkey']
for idx, animal in enumerate(animals):
    print('#%d: %s' % (idx + 1, animal))
# Prints "#1: cat", "#2: dog", "#3: monkey", each on its own line
```

**列表综合式(List comprehensions)** ：在编程的时候，我们常常想要将一种数据类型转换为另一种。下面是一个简单例子，将列表中的每个元素变成它的平方。

```python
nums = [0, 1, 2, 3, 4]
squares = []
for x in nums:
    squares.append(x ** 2)
print(squares)   # Prints [0, 1, 4, 9, 16]
```


