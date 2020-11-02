---
title: IPythonStudy
date: 2020-10-26 09:13:48
tags: 
	- Python
	- IPython
---

# [手册](https://www.runoob.com/manual/pythontutorial3/docs/html/)

# pip命令

* 显示版本和路径

  ```python
  pip --version
  ```

* 获取帮助

  ```python
  pip --help
  ```

* 升级pip

  ```python
  pip install -U pip
  ```

* 安装其它包

  ```python
  pip install SomePackage           #最新版本
  ```

  ```python
  pip install SomePackage==1.0.4    #指定版本
  ```

  ```python
  pip install 'SomePackaage>=1.0.4' #最小版本
  ```

* 升级包

  ```python
  pip install --upgrade SomePackage
  ```

* 卸载包

  ```python
  pip uninstall SomePackage
  ```

* 搜索包

  ```python
  pip search SomePackage
  ```

* 显示安装包信息

  ```python
  pip show SomPackage
  ```

* 查看指定包的详细信息

  ```python
  pip show -f SomePackage
  ```

* 列出已安装的包

  ```python
  pip list
  ```

* 查看可升级的包

  ```python
  pip list -o
  ```

# 注释

* 使用“#”号
* 使用一对三个单引号，一对三个双引号

# 函数

```python
def 函数名(参数1，参数2，参数3...)
	函数体
    return 返回的值
```

# Python模块的导入及使用

```python
import numpy
numpy.sqrt(4)
```

```sql
import numpy as np
np.sqrt(4)
```

```python
from numpy import sqrt,exp
sqrt(4)
exp(3)
```

# itertools包中product函数

```python
from itertools import product
for i,j in product(range(4),range(4))
{
    print (i,j);
}

#相当于
for i in range(4):
    for j in range(4):
        print (i,j);
```

# math包中的sqrt函数

# 分支结构

```python
if condition1:
    
elif condition2:

else:
```

# 运算符

* //运算符，浮点数除法去除小数部分只留下整数部分
* \*\*运算符，计算幂乘方

# 交互模式中，最近一个表达式的值赋值给变量 _

```python
>>> tax = 12.5 / 100
>>> price = 100.50
>>> price * tax
12.5625
>>> price + _
113.0625
>>> round(_, 2)
113.06
```

# range()函数

```python
for i in range(4):
    print(i)
```

# 录入数据

```python
变量 = int(input('提示内容'))
```

# 列表

```python
list.append(x)

list.extend(L)
#将一个给定列表中的所有元素都添加到另一个列表中
list.insert(i,x)
list.insert(len(a),x)#相当于a.append(x)
#在指定位置插入一个元素,i为下标(从0开始)
list.remove(x)
#删除列表中值为x的第一个元素。如果没有这样的元素，就会返回一个错误
list.pop([i])#这个方括号的意思是可以省略
#从列表的指定位置删除元素，并将其返回。如果没有指定索引，a.pop()返回最后一个元素。元素随机从列表中被删除
list.clear()
#从列表中删除所有元素。相当于del a[:]
list.index(x)
#返回列表中第一个值为x的元素的索引。如果没有匹配的元素就会返回一个错误
list.count(x)
#返回x在列表中出现的次数
list.sort()
#对列表中的元素就地进行排序（意思是原来的顺序不在了）
list.reverse()
#就地倒排列表中的元素
list.copy()
#返回列表的一个浅拷贝。等同于a[:]
```

# 浅拷贝和深拷贝

* 看下面的实例

```python
colours1 = ["red", "blue"]
colours2 = colours1
print(colours1)
print(colours2)
print(id(colours1), id(colours2))
```

​	输出结果

```python
['red', 'blue']
['red', 'blue']
563841065096 563841065096
```

> 两个列表指向的是同一块地址

* 现在来看看赋值给colours2一个新的列表对象，会发生什么

```python
colours2 = ["rouge", "vert"]
print(colours1)
print(colours2)
print(id(colours1), id(colours2))
```

​	输出结果

```python
['red', 'blue']
['rouge', 'vert']
357368848712 357368848456
```

> colour2被重新分配了地址，colour1没变

* 现在修改colour2中的一个值

```python
colours1 = ["red", "blue"]
colours2 = colours1
print(id(colours1), id(colours2))
colours2[1] = "green"
print(id(colours1), id(colours2))
print(colours1)
print(colours2)
```

​	输出结果

```python
1026592727752 1026592727752
1026592727752 1026592727752
['red', 'green']
['red', 'green']
```

> 这是两个列表都被改变了，此时两个对象指向的还是同一块地址

* 使用a[:]得到一份副本（浅拷贝的副本）

```python
list1 = ['a', 'b', 'c', 'd']
list2 = list1[:]
list2[1] = 'x'
print(list2)
print(list1)
```

​	输出结果

```python
['a', 'x', 'c', 'd']
['a', 'b', 'c', 'd']
```

> list2 = list1[:]，是产生了一个list1的副本，这个新的对象中的值是list1中的浅拷贝。这里还体现不出来，如果是一个嵌套列表的话就可以体现出来，如下：

```python
lst1 = ['a', 'b', ['ab', 'ba']]
lst2 = lst1[:]
lst2[0] = 'c'
print(lst1)
print(lst2)
```

​	输出结果

```python
['a', 'b', ['ab', 'ba']]
['c', 'b', ['ab', 'ba']]
```

​	但是如果改变的是嵌套子列表中的值，情况就发生了变化。

```python
lst2[2][1] = 'd'
print(lst1)
print(lst2)
```

​	输出结果

```python
['a', 'b', ['ab', 'd']]
['c', 'b', ['ab', 'd']]
```

> 原因是前面将的a[:]只是产生一个a的浅拷贝的副本，意思就是简单赋值一下每个元素的值，所以前面的'a'和'b'会被赋值，然后后面那个嵌套的子列表也只是地址被复制了过去，所以再去引用的时候，lst1和lst2的嵌套子列表指向的是同一块地址。

* 所以遇到嵌套子列表的列表，要使用深复制

```python
from copy import deepcopy
lst1 = ['a', 'b', ['ab', 'ba']]
lst2 = deepcopy(lst1)
print(lst1)
print(lst2)
print(id(lst1))
print(id(lst2))
print(id(lst1[0]))
print(id(lst2[0]))
print(id(lst1[2]))
print(id(lst2[2]))
```

​	输出结果

```python
['a', 'b', ['ab', 'ba']]
['a', 'b', ['ab', 'ba']]
537508176136
537508176200
537506121184
537506121184
537508176712
537508176776
```

> 此时lst1和lst2就没有什么关联了。

# 元组

* 一个元组由数个逗号分隔的值组成。
* 元组的值是不可更改的

```python
>>>t = 12345,54321,'hello'
>>>t[0]
12345
>>>t
(12345,54321,'hello')
#元组可以嵌套
>>>u = t,(1,2,3,4,5)
>>>u
((12345,54321,'hello'),(1,2,3,4,5))
#元组的值是不可更改的，会报错

```

