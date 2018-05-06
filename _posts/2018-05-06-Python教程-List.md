---
layout:       post
title:        "Python教程-List"
subtitle:     "Python tutorial-List"
date:         2018-05-06 11:10:00
author:       "xuepro"
header-img:   "img/home_bg.jpg"
header-mask:  0.3
catalog:      true
multilingual: true
tags:
    - Python 
    
---    
     
## List

表示一列元素，用于将不同的值组合在一起，所有元素可以写在一对方括号[]里并以逗号','隔开。这些元素的数据类型可以不同。例如
   
  


```python
squares = [1, 4, 9, 16, 25]
my_list = [1, "Hello", 3.4]
print(squares)
print(my_list)
```

    [1, 4, 9, 16, 25]
    [1, 'Hello', 3.4]
    

既然List可以有不同类型的数据元素，List里当然还可以包含替他的List，例如：


```python
my_list = ["mouse", [8, 4, 6], ['a']]
```

可以用下标运算符[]去访问List的数据元素，下标从0开始，长度为len的最后一个元素的下标是len-1。


```python
print(my_list)
print(my_list[0])
print(my_list[2])
print(my_list[1][2])
```

    mouse
    ['a']
    6
    

下标也可以是负数，最后一个元素的下标是-1,倒数第2个元素的下标是-2,...


```python
print(my_list)
print(my_list[-1])
print(my_list[-2])
```

    ['mouse', [8, 4, 6], ['a']]
    ['a']
    [8, 4, 6]
    

下标不能超出范围，比如正的下标应该属于[0,len(my_list)-1]，而负的下标应该属于[-len(my_list),-1]，例如


```python
print(my_list)
print(my_list[2])      #最后一个元素,等价于 print(my_list[ len(my_list)-1]
print(my_list[ len(my_list)-1])

print(my_list[-3])    #第一个元素,等价于 print(my_list[ -len(my_list)]
print(my_list[-len(my_list)])
```

    ['mouse', [8, 4, 6], ['a']]
    ['a']
    ['a']
    mouse
    mouse
    


```python
#下标超出范围
print(my_list[3])
print(my_list[-4])
```

```python
    ------------------------------------------------

    IndexError     Traceback (most recent call last)

    <ipython-input-23-79c6594a505b> in <module>()
          1 #下标超出范围
    ----> 2 print(my_list[3])
          3 print(my_list[-4])
    

    IndexError: list index out of range
```

可以用过切片操作(slicing operator)即冒号:(colon)访问一个范围的多个元素，格式为：
```python
   list[start:end]
```
表示查询从start到end之间(但不包含end)的那些元素。

如果省略start，表示从第一个（下标0）开始，如果省略end，表示end是最后一个元素的后一个位置。即查询从start开始往后的所有元素！

例如


```python
my_list = ['p','r','o','g','r','a','m','i','z']
# elements 3rd to 5th
print(my_list[2:5])  #从第3个到第5个，不包含第5个

# elements beginning to 4th
print(my_list[:-5])  #从开头到倒数第5个，不包含倒数第5个

# elements 6th to end
print(my_list[5:])   #从第6个往后的所有元素

# elements beginning to end
print(my_list[:])     #所有元素
```
```python
    ['o', 'g', 'r']
    ['p', 'r', 'o', 'g']
    ['a', 'm', 'i', 'z']
    ['p', 'r', 'o', 'g', 'r', 'a', 'm', 'i', 'z']
```    

可以用下面的图理解正负下标

![](https://cdn.programiz.com/sites/tutorial2program/files/element-slicling.jpg)

List是可以修改的（mutable），我们可以通过下标(切片)修改其中的一个或多个元素。
对切片的修改还有“插入”或“删除”的效果，例如


```python
my_list = ['p','r','o','g','r','a','m','i','z']
my_list[1] = 34
print(my_list)
```
```python
    ['p', 34, 'o', 'g', 'r', 'a', 'm', 'i', 'z']
```   


```python
my_list[2:6] = [25,8]  #用一个新的list[25,8]替换切片my_list[2:6]
print(my_list)
```

```python
    ['p', 34, 25, 8, 'm', 'i', 'z']
```   

```python
my_list[2:5]=[]  #用一个空的list替换切片，相当于删除切片中的数据元素
print(my_list)
```
```python
    ['p', 34, 'i', 'z']
 ```   


```python
my_list[2:2]=["hello","world"] #相当于在下标2除插入一组元素
print(my_list)
```
```python
    ['p', 34, 'hello', 'world', 'i', 'z']
```    

我们还可以通过list的方法，比如append()在list最后添加一个元素或用extend()添加所个元素。例如



```python
odd = [1, 3, 5]

odd.append(7)

# Output: [1, 3, 5, 7]
print(odd)

odd.extend([9, 11, 13])

# Output: [1, 3, 5, 7, 9, 11, 13]
print(odd)
```

    [1, 3, 5, 7]
    [1, 3, 5, 7, 9, 11, 13]
    

也可以通过加法```+```运算符拼接2个list，用乘法```*```运算符复制多个list 例如


```python
odd = [1, 3, 5]

# Output: [1, 3, 5, 9, 7, 5]
print(odd + [9, 7, 5])

#Output: ["re", "re", "re"]
print(["re"] * 3)
```

可以用insert方法在中间某个位置插入一个元素


```python
odd = [1, 9]
odd.insert(1,3)
print(odd)        # Output: [1, 3, 9] 

odd.insert(1,[4,5])
print(odd)
```

    [1, 3, 9]
    [1, [4, 5], 3, 9]
    

同样，我们可以用del函数删除一个元素或一个范围的元素(切片)。当del作用域整个list时，这个list对象就被系统回收，不存在了。


```python
my_list = ['p','r','o','b','l','e','m']

# delete one item
del my_list[2]

# Output: ['p', 'r', 'b', 'l', 'e', 'm']     
print(my_list)

# delete multiple items
del my_list[1:5]  

# Output: ['p', 'm']
print(my_list)

# delete entire list
del my_list       

# Error: List not defined
print(my_list)
```
```python
    ['p', 'r', 'b', 'l', 'e', 'm']
    ['p', 'm']
    


    ------------------------------------------------

    NameError      Traceback (most recent call last)

    <ipython-input-36-6ea590b7a951> in <module>()
         17 
         18 # Error: List not defined
    ---> 19 print(my_list)
    

    NameError: name 'my_list' is not defined


```


可以通过remove删除特定的元素，注意：此时传递给remove的是这个元素的值而不是下标


```python
my_list = ['p','r','o','b','l','e','m']
my_list.remove('p')

# Output: ['r', 'o', 'b', 'l', 'e', 'm']
print(my_list)


# animal list
animal = ['cat', 'dog', 'rabbit', 'guinea pig']

# 'rabbit' element is removed
animal.remove('rabbit')

#Updated Animal List
print('Updated animal list: ', animal)
```

```python

 ['r', 'o', 'b', 'l', 'e', 'm']
 Updated animal list:  ['cat', 'dog', 'guinea pig']
 
``` 

List的pop方法可以删除指定下标的元素，如果没有指定下标，则删除最后一个元素。而clear()方法则清空整个list，但没有销毁它


```python
my_list = ['p','r','o','b','l','e','m']
my_list.pop(2)
print(my_list)
my_list.pop()
print(my_list)
my_list.clear()
print(my_list)
```
```python
    ['p', 'r', 'b', 'l', 'e', 'm']
    ['p', 'r', 'b', 'l', 'e']
    []
 ```   

### Python List Methods

```
append() - Add an element to the end of the list
extend() - Add all elements of a list to the another list
insert() - Insert an item at the defined index
remove() - Removes an item from the list
pop() - Removes and returns an element at the given index
clear() - Removes all items from the list
index() - Returns the index of the first matched item
count() - Returns the count of number of items passed as an argument
sort() - Sort items in a list in ascending order
reverse() - Reverse the order of items in the list
copy() - Returns a shallow copy of the list
```

**sort方法**

```

list.sort(key=..., reverse=...)  #修改原List
```
或
```
sorted(list, key=..., reverse=...) #不修改原List,返回一个 iterable list
```
**sort()的参数Parameters**

* **reverse** - 如是是true,则以逆序(下降次序)排序 

* **key** -- 是一个函数对象，用作排序比较的关键字 function that serves as a key for the sort comparison
           即根据这个作用于每个元素的函数的结果值进行比较




```python
vowels = ['e', 'a', 'u', 'o', 'i']

vowels.sort()  #以正序排序

print('Sorted list:', vowels)
```
```python
    Sorted list: ['a', 'e', 'i', 'o', 'u']
```   


```python
vowels.sort(reverse=True)   # 以逆序排序

print('Sorted list (in Descending):', vowels)
```
```
    Sorted list (in Descending): ['u', 'o', 'i', 'e', 'a']
 ```   


```python
# take second element for sort
def takeSecond(elem):
    return elem[1]

pairs = [(1, 'one'), (2, 'two'), (3, 'three'), (4, 'four')]

pairs.sort(key=takeSecond)  #key是一个用于比较的关键字函数，即根据这个作用于每个元素的函数的结果值进行比较

print('Sorted list:', pairs)
```

```python
Sorted list: [(4, 'four'), (1, 'one'), (3, 'three'), (2, 'two')]
    
```


也可以用lambda函数代替普通的函数：


```python
pairs = [(1, 'one'), (2, 'two'), (3, 'three'), (4, 'four')]

pairs.sort(key=lambda pair: pair[1])

print('Sorted list:', pairs)
```

    Sorted list: [(4, 'four'), (1, 'one'), (3, 'three'), (2, 'two')]
    

### Built-in Functions with List

```
all()	Return True if all elements of the list are true (or if the list is empty).
any()	Return True if any element of the list is true. If the list is empty, return False.
enumerate()	Return an enumerate object. It contains the index and value of all the items of list as a tuple.
len()	Return the length (the number of items) in the list.
list()	Convert an iterable (tuple, string, set, dictionary) to a list.
max()	Return the largest item in the list.
min()	Return the smallest item in the list
sorted()	Return a new sorted list (does not sort the list itself).
sum()	Return the sum of all elements in the list.
```

### List Comprehension: 

创建list的优雅的方式


```python
pow2 = [2 ** x for x in range(10)]

# Output: [1, 2, 4, 8, 16, 32, 64, 128, 256, 512]
print(pow2)
```

    [1, 2, 4, 8, 16, 32, 64, 128, 256, 512]
    

等价于


```python
pow2 = []
for x in range(10):
   pow2.append(2 ** x)
print(pow2)
```

    [1, 2, 4, 8, 16, 32, 64, 128, 256, 512]
    
### 对list的其他操作

用in判断一个元素是否在一个list里


```python
my_list = ['p','r','o','b','l','e','m']
print('p' in my_list)

# Output: False
print('a' in my_list)

# Output: True
print('c' not in my_list)
```

    True
    False
    True
    

用for迭代遍历一个list


```python
for fruit in ['apple','banana','mango']:
    print("I like",fruit)
```

    I like apple
    I like banana
    I like mango
    


```python

```
