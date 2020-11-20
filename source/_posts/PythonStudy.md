---
title: PythonStudy
date: 2020-11-12 09:46:42
tags: python
categories: python
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

# 列表list

* list[:,1]

```python
[[1，2，3]
[4，5，6]
[7、8、9]]
list[1,1] -->  5 # it says select the element in position [1,1] (note that indexes start from zero)
list[:,1] --> [2,5,8] 
list[1][1]  --> 5
list[:][1] --> [4 5 6]
```

* `plt.scatter(X_test[:,0],X_test[:,1],c=[color_dict[i] for i in y_])` 

  链表推导式：

  `x for x in x`

  ```python
  >>>vec = [2,4,6]
  >>>[3*x for x in vec]
  [6,12,18]
  >>>[3*x for x in vec if x<2]
  []
  >>>[[x,x**2]for x in vec]        #list嵌套
  [[2,4],[4,16],[6,36]]
  >>>[(x,x**2)for x in vec]        #元素为元组
  [(2,4),(4,16),(6,36)]
  >>> vec1 = [2, 4, 6]
  >>> vec2 = [4, 3, -9]
  >>>[x*y for x in vec1 for y in vec2]
  [8,6,-18,16,12,-36,24,18,-54]
  >>> [vec1[i]*vec2[i] for i in range(len(vec1))]
  [8, 12, -54]
  
  为使链表推导式匹配for循环的行为，可以在推导之外保留循环变量：
  >>> x = 100 # this gets overwritten
  >>> [x**3 for x in range(5)]
  [0, 1, 8, 27, 64]
  >>> x # the final value for range(5)
  ```

* mylist = list('abcde')

  ```python
  >>>mylist = list('abcde')
  >>>print(mylist)
  ['a','b','c','d','e']
  >>>mylist = list(['abcde'])
  >>>print(mylist)
  ['abcde']
  ```

# pandas中series和datagram

* pandas 是基于 NumPy 的一个 Python 数据分析包，主要目的是为了数据分析。它提供了大量高级的数据结构和对数据处理的方法。

  pandas 有两个主要的数据结构：

  * **Series** 
  * **DataFrame**

* **series**

  * Series 是一个一维数组对象 ，类似于 NumPy 的一维 array。它除了包含一组数据还包含一组索引，所以可以把它理解为一组带索引的数组

    * 将python数组转换成Series对象：

      默认索引为从零开始的数字

      ```python
      >>>from pandas import Series,DataFrame
      >>>import Pandas as pd
      >>>obj = Series([2,3,4,-5])
      >>>obj
      0 2
      1 3
      2 4
      3 -5
      dtype:int64
      ```

    * 将python字典转换成Series对象：

      则指定了索引的值

      ```python
      >>>dic = {'a':1,'b':2,'c':3,'d':4}
      >>>obj3 = Series(dic)
      >>>obj3
      a 1
      b 2
      c 3
      d 4
      dtype:int64
      ```

    * 当没有显示指定索引的时候，Series 自动以 0 开始，步长为 1 为数据创建索引。

      你也可以通过 index 参数显示指定索引：

      ```python
      >>>obj2 = Series([2,3,4,-5],index=['a','b','c','d'])
      >>>obj2
      a 2
      b 3
      c 4
      d -5
      ```

    * 对于 Series 对象里的单个数据来说，和普通数组一样，根据索引获取对应的数据或重新赋值；

      不过你还可以传入一个`索引的数组` 来获取数组中值作为索引对应的值或为数组中的值作为索引的数据重新赋值

      ```python
      >>>obj2['a']
      2
      >>>obj2[['a','b']]
      a 2
      b 3
      >>>obj2['a']=10
      >>>obj2
      a 10
      b 3
      c 4
      d -5
      >>>obj2[['b','c','d']]=20
      >>>obj2
      a 10
      b 20
      c 20
      d 20
      ```

    * 单独获取Series对象的索引或者数组内容的时候，可以使用index和values属性

      ```python
      >>>obj2.index
      Index([u'a',u'b',u'c',u'd'],dtype='object')
      >>>obj2.values
      array([2,3,4,-5])
      ```

    * 对series对象的运算(索引不变)

      ```python
      >>>obj2*2
      a 20
      b 40
      c 40
      d 40
      >>>obj2+1
      a 11
      b 21
      c 21
      d 21
      >>>obj2[obj2 <= 10]
      a 10
      >>>obj2[obj2 > 10]
      b 20
      c 20
      d 20
      ```

* **DataFrame**

  DataFrame 是一个表格型的数据结构。它提供`有序的列`和`不同类型的列值`。

  例如将一个由字典组成的字典转换成 DataFrame 对象：

  ```python
  >>>data = {'name':['Carl','Peter','Lucy','Job'],'age':[30,34,20,35],'gender':['m','m','f','m']}
  >>>frame = DataFrame(data)
  >>>frame
  	age gender name
  0   30      m   Carl
  1   34      m  Peter
  2   20      f   Lucy
  3   35      m    Job
  ```

  * DataFrame默认根据列名首字母顺序对列名进行排序，也可以指定列的顺序

    ```python
    >>>frame = DataFrame(data,columns=['name','age','gender'])
    >>>frame
       name age gender
    0  Carl 30      m 
    1  Peter34      m 
    2  Lucy	20      f 
    3  Job	35      m 
    ```

  * 如果传入的列名找不到，会产生一列NA值

    ![image.png](https://i.loli.net/2020/11/12/AHaOEl3ZpLwdF2v.png)

  * DataFrame不仅可以以字典索引的方式获取数据，还可以以属性的方法获取

    ![image.png](https://i.loli.net/2020/11/12/1LAMRzkPSXmp4wu.png)

  * 修改列的值

    ![image.png](https://i.loli.net/2020/11/12/dpBi4yc7q2MDELX.png)

  * 删除某一列

    ![image.png](https://i.loli.net/2020/11/12/ceA3FPaQjplTsxU.png)

  * 通过columns属性获得index，通过values属性返回numpy.ndarray，可以通过.tolist()或者list()转换成列表

    ```python
    print(type(df.columns))
    <class 'pandas.core.indexes.base.Index'>
    print(type(df.columns.values))
    <class 'numpy.ndarray'>
    print(type(df.columns.tolist()),":"+"\n",df.columns.tolist())
    <class 'list'> :
     ['a', 'b']
    print(type(df.columns.values.tolist()),":"+"\n",df.columns.values.tolist())
    <class 'list'> :
     ['a', 'b']
    ```

  * 通过链表推导式获得index

    ```python
    [column for column in df]
    [a,b]
    ```

  * 直接使用list，返回一个含有columns的list列表

    ```python
    print(list(df))
    ['a', 'b']
    ```

  * 通过datagram.values属性获得datagrame的值(不包括header)

    ```python
    print(df.values)
    ```

# DataFrame进行排序

* 一个比较重要的参数是 *axis* 。

  它指定的在 *0轴* 还是 *1轴* 上来进行排序，默认 axis=0。
  
  这个参数在计算的时候也会用到，从文字上来讲，就是 *0轴* 是“跨过”一行一行来进行处理，所以排序指定 *0轴* 就是把每一行当作一个单位

  比较指定列（所以axis=0时候，要指定列索引）上的数值，来进行排序。反之指定 *1轴* 相反。

* ![image.png](https://i.loli.net/2020/11/12/9tidFELWNm1YehO.png)

* 按照列名排序(默认)

  ```python
  df1.sort_index(axis=1)
  ```

  按照索引排序

  ```python
  df1.sort_index()
  ```

  ![image.png](https://i.loli.net/2020/11/12/vgkCqbPo2lxV5Q4.png)

* 按照列名或者索引进行降序排序

  添加参数ascending = False
  
  ![image.png](https://i.loli.net/2020/11/12/D6Ny7HUhEoKilk9.png)
  
* 根据一列或多列的值进行排序

* ![image.png](https://i.loli.net/2020/11/12/pKy7VMCQUeIvctz.png)

* `df2.sort_values(by='b')`对df2按照b列排序，

  `df2.sort_values(by=['b','a'])`对df2按照b列排序后如有相同的再按照a列排序，
  
  `df2.sort_values(by=['a','b'])`对df2按照a列排序后如有相同的再按照b列排序，
  
  ![image.png](https://i.loli.net/2020/11/12/Bpwu7RYXAnmrLGa.png)
  
* DataFrame列出排名。

  df2按照索引和列排序分别用`df2.rank()`和`df2.rank(axis=1)`即可，如图

  ![image.png](https://i.loli.net/2020/11/12/gV1olBDu4ZAvQRP.png)

* 若排序不成功，则可能是没有替换原来的文本

  再在后面添加参数`inplace = True` 

  

# list和numpy.array的区别

- Numpy是专门针对数组的操作和运算进行了设计，所以数组的存储效率和输入输出性能远优于Python中的嵌套列表，**数组越大，Numpy的优势就越明显**。**通常Numpy数组中的所有元素的类型都是`相同的`，而Python列表中的元素类型是任意的，所以在通用性能方面Numpy数组不及Python列表，但在科学计算中，可以省掉很多循环语句，代码使用方面比Python列表简单的多。**

- 在list中的数据类型保存的是数据的存放的地址，简单的说就是指针，并非数据，这样保存一个list就太麻烦了，例如list1=[1,2,3,‘a’]需要4个指针和四个数据，**增加了存储和消耗cpu。**

- 程序举例

  - 创建

    - 列表的创建

      ```python
      >>>x = list()
      >>>x.append(1)
      >>>x.extend([2,3,4])
      >>>print(x)
      x = [1,2,3,4,5]
      ```

      > list.append()和list.extend()的区别，append将()内所有的内容当作**一个元素** 加入到列表中，而extend是一个一个加

    - numpy数组创建

      ```python
      import numpy as np
      a = np.array((1,2,3))               #参数为tuple
      b = np.array([6,7,8])				#参数为list
      c = np.array([[1,2,3],[4,5,6]])     #参数是二维list
      
      #其它方法创建
      arr1 = np.arrange(1,10,1)
      arr2 = np.linspace(1,10,10)
      ```

      * np.arrange(a,b,c)表示产生从[a,b)，间隔为c的一个array，数据类型默认是int32
      * linspace(a,b,c)表示的是把[a,b]平均分成c份

  - 元素访问

    - 一维数组、列表访问(一样)

      ![image.png](https://i.loli.net/2020/11/12/1BWEYTOwsfz86oa.png)

    - 二维数组、列表访问

      ![image.png](https://i.loli.net/2020/11/12/fdF63p5G8smVWJl.png) 

      * 列表

        ```python
        >>>x = [[1,2,3],[4,5,6]]
        >>>print(x[1:2])
        >>>print(x[1:2][0])
        >>>print(x[1])
        >>>print(x[0][0])
        ```

      * numpy.array

        ```python
        >>>x=np.array([[1,2,3],[4,5,6]])
        >>>print(x[1:2])
        >>>print(x[1:2][0])
        >>>print(x[1])
        >>>print(x[0][0])
        >>>print(x[0,0])
        ```

      * 区别：在列表List中，不能使用x[0,0]来访问第一行第一列的元素，只能使用x\[0\]\[0\]

  - numpy.array中的二维数组(逗号,)

    - X[n0,n1]是通过 numpy 库引用二维数组或矩阵中的某一段数据集的一种写法。
      类似的，X[n0,n1,n2]表示取三维数组，取N维数组则有N个参数，N-1个逗号分隔。

    - #### 取元素 X[n0,n1]

      这是最基本的情况，表示取 第0维 的第 n0 个元素，继续取 第1维 的第 n1个元素。如 X[2,2] 表示第0维第2个元素[20,21,22,23],然后取其第1维的第2个元素即 22；

    - #### 切片 X[s0:e0,s1:e1]

      这是最通用的切片操作，表示取 第0维 的第 s0 到 e0 个元素，继续取 第1维 的第 s1 到 e1 个元素（左闭右开）。如 X[1:3,1:3] 表示第0维第(1:3)个元素[[10,11,12,13],[20,21,22,23]],然后取其第1维的第(1:3)个元素即 [[11,12],[21,22]]；

    - #### 切片特殊情况 X[:e0,s1:]

      特殊情况，即左边从0开始可以省略X[:e0,s1:e1]，右边到结尾可以省略X[s0:,s1:e1]，取某一维全部元素X[:,s1:e1]，事实上和Python 的 序列切片规则是一样的。

      常见的 X[:,0] 则表示 第0维取全部，第1维取0号元素；

  - **list中的切片最好在一个维度上进行切片**

  * 浅拷贝与深拷贝

    * numpy.array中存放的是数据元素的地址，所以利用切片进行浅拷贝的时候，复制的都是地址，所以浅拷贝后改变没有嵌套数组的值，原来数组的值也会改变。

      numpy.array存放的元素必须是相同的类型，所以有嵌套的话就是多维数组了。

    * numpy的深复制为

      ```python
      >>>import numpy as np
      >>>x = np.array([[1,2,3],[4,5,6]])
      >>>x1 = x[:][:].copy()
      >>>x1[1,1] = 1
      >>>print(x1)
      [[1 2 3]
       [4 1 6]]
      >>>print(x)
      [[1 2 3]
       [4 5 6]]
      ```

    * list中存放的是这个元素的值，如果这个元素是列表，那么存放的是list的地址，所以如果是没有嵌套的话，改变浅拷贝的值不改变原来的值

      如果有嵌套的话，list就要进行深复制

      ```python
      lst1 = ['a', 'b', ['ab', 'ba']]
      lst2 = deepcopy(lst1)
      ```

# list和numpy.array的切片

* 一维切片

  比较简单，就不过多叙述

* 二维形式切片

  * list

    > list的切片只能在一个维度上进行，即使写了多个维度，但是还是按照从前往后的顺序进行切片，而且把list当作一个大的整体的一个list，即其中的嵌套也是一个元素

    ```python
    >>>x = [[1,2,3],[4,5,6]]
    >>>print(x[:])
    [[1,2,3],[4,5,6]]
    >>>print(x[:][:1])
    [[1,2,3]]
    >>>print(x[:][:2][:1])
    [[1,2,3]]
    >>>print(x[:][:2][:1][:0])
    []
    ```

  * numpy.array

    > 如果切片的写法和上面那个list的写法一样，那么效果是一样的，还是多个一维的切片

    ```python
    >>>import numpy as np
    >>>x = np.array([[1,2,3],[4,5,6]])
    >>>print(x[:])
    [[1,2,3],[4,5,6]]
    >>>print(x[:][:1])
    [[1,2,3]]
    >>>print(x[:][:2][:1])
    [[1,2,3]]
    >>>print(x[:][:2][:1][:0])
    []
    ```

    > 如果切片形式是[,]形式，则是真正的多维度切片

    ```python
    >>>import numpy as np
    >>>x = np.array([[1,2,3],[4,5,6]])
    >>>print(x[:,1])
    [2 5]
    >>>print(x[:,:2])
    [[1 2]
     [4 5]]
    ```

# numpy.ndarray的降维

* array.ravel()

  将高维数组降维到一维

# python字典

* 字典是零一中可变容器模型，且`可存储任意类型对象` 

* 字典的每个键值对`key=>value` 用冒号分隔，每个对之间用逗号(,)分割，整个字典包括在花括号`{}` 中，格式如下所示：

  ```python
  d = {key1:value1,key2:value2,key3:value3}
  ```

* 键是唯一的，但值不必

* 值可以取任何数据类型，但键必须是不可变的，如字符串，数字。

  ```python
  dict1 = {'abc':456}
  dict2 = {'abc':123,98.6:37}
  ```

* 访问字典里的值

  把相应的键放入方括号中，如下：

  ```python
  >>>dict = {'name':'runoob','age':7,'class':'First'}
  >>>print(dict['name'])
  runoob
  >>>print(dict['age'])
  7
  ```

* 修改字典

  ```python
  >>>dict['age'] = 8             # 更新Age
  >>>dict['school'] = '菜鸟教程'  # 添加信息
  >>>del dict['name']            # 删除键值对'name'=>'runoob'
  >>>del dict                    # 删除字典
  ```

* 字典键的特性

  * 不允许同一个键出现两次。创建时如果同一个键被赋值两次，后一个值会被记住

  * 键必须不可变，所以可以用数字，字符串或`元组` 充当，而用`列表`就不行，如下实例：

    ```python
    >>>dict = {['Name']: 'Runoob', 'Age': 7}
    >>>print ("dict['Name']: ", dict['Name'])
    Traceback (most recent call last):
      File "test.py", line 3, in <module>
        dict = {['Name']: 'Runoob', 'Age': 7}
    TypeError: unhashable type: 'list'
    ```

* python字典内置函数和方法

  * 内置函数

    * len(dict)

      计算字典元素的个数，即键的总数

      ```python
      >>> dict = {'Name': 'Runoob', 'Age': 7, 'Class': 'First'}
      >>> len(dict)
      3
      ```

    * str(dict)

      输出字典，以可打印的字符串表示

      ```python
      >>> dict = {'Name': 'Runoob', 'Age': 7, 'Class': 'First'}
      >>> str(dict)
      "{'Name': 'Runoob', 'Class': 'First', 'Age': 7}"
      ```

    * type(variable)

      返回输入的变量类型，如果变量是字典就返回字典类型

      ```python
      >>> dict = {'Name': 'Runoob', 'Age': 7, 'Class': 'First'}
      >>> type(dict)
      <class 'dict'>
      ```

  * 内置方法

    * dict.clear()

      删除字典内所有元素

    * dict.copy

      返回字典的一个浅拷贝

      浅拷贝参照前面的笔记

    * dict.fromkeys()

      ```python
      >>>seq = ('name', 'age', 'sex')
      >>>dict = dict.fromkeys(seq)#默认值为None
      >>>print ("新的字典为 : %s" %  str(dict))
      新的字典为 : {'age': None, 'name': None, 'sex': None}
      >>>dict = dict.fromkeys(seq, 10)
      >>>print ("新的字典为 : %s" %  str(dict))
      新的字典为 : {'age': 10, 'name': 10, 'sex': 10}
      ```

    * dict.get(key,default=None)

      返回指定键的值，如果键不在字典中则返回default设置的默认值

      ```python
      >>>dict = {'Name': 'Runoob', 'Age': 27}
      >>>print ("Age 值为 : %s" %  dict.get('Age'))
      Age 值为 : 27
      >>>print ("Sex 值为 : %s" %  dict.get('Sex', "NA"))
      Sex 值为 : NA
      ```

    * key in dict

      如果键在字典dict里则返回true，反之返回false

      ```python
      >>>dict = {'Name': 'Runoob', 'Age': 7}
      # 检测键 Age 是否存在
      >>>if  'Age' in dict:
             print("键 Age 存在")
         else :
             print("键 Age 不存在")
      键 Age 存在
      ```

    * dict.items()

      返回可便利的(键，值)`元组`数组

      ```python
      >>>dict = {'Name': 'Runoob', 'Age': 7}
      >>>print ("Value : %s" %  dict.items())
      Value : dict_items([('Age', 7), ('Name', 'Runoob')])
      ```

    * dict.keys()

      ```python
      >>> dict = {'Name': 'Runoob', 'Age': 7}
      >>> dict.keys()
      dict_keys(['Name', 'Age'])
      >>> list(dict.keys())             # 转换为列表
      ['Name', 'Age']
      ```

    * dict.setdefault(key,default=None)

      和get()类似, 但如果键不存在于字典中，将会添加键并将值设为default

      ```python
      >>>dict = {'Name': 'Runoob', 'Age': 7}
      >>>print ("Age 键的值为 : %s" %  dict.setdefault('Age', None))
      Age 键的值为 : 7
      >>>print ("Sex 键的值为 : %s" %  dict.setdefault('Sex', None))
      Sex 键的值为 : None
      >>>print ("新字典为：", dict)
      新字典为： {'Age': 7, 'Name': 'Runoob', 'Sex': None}
      ```

    * dict.update(dictw)

      ```python
      >>>dict = {'Name': 'Runoob', 'Age': 7}
      >>>dict2 = {'Sex': 'female' }
      >>>dict.update(dict2)
      >>>print ("更新字典 dict : ", dict)
      更新字典 dict :  {'Name': 'Runoob', 'Age': 7, 'Sex': 'female'}
      ```

    * dict.values()

      ```python
      >>>dict = {'Sex': 'female', 'Age': 7, 'Name': 'Zara'}
      >>>print ("字典所有值为 : ",  list(dict.values()))
      字典所有值为 :  ['female', 7, 'Zara']
      ```

    * dict.pop(key[,default]) []为可省略内容

      删除字典给定键key所对应的值，返回值为被删除的值。

      key必须给出，否则返回default值

      ```python
      >>> site= {'name': '菜鸟教程', 'alexa': 10000, 'url': 'www.runoob.com'}
      >>> pop_obj=site.pop('name')
      >>> print(pop_obj)
      菜鸟教程
      ```

    * dict.popitem()

      以先进先出规则返回一个键值对，所以返回的是最后一个键值对。然后将最后的键值对删除。

      ```python
      >>>site= {'name': '菜鸟教程', 'alexa': 10000, 'url': 'www.runoob.com'}
      >>>pop_obj=site.popitem()
      >>>print(pop_obj)  
      ('url', 'www.runoob.com')
      >>>print(site)
      {'name': '菜鸟教程', 'alexa': 10000}
      ```

# [补笔记](https://blog.csdn.net/weixin_47021806/article/details/108302282?utm_medium=distribute.pc_aggpage_search_result.none-task-blog-2~all~sobaiduend~default-2-108302282.nonecase&utm_term=python%20%E9%81%8D%E5%8E%86%E5%AD%97%E5%85%B8%E5%89%8Dn%E4%B8%AA&spm=1000.2123.3001.4430)







