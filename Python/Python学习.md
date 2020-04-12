

# Python学习

https://github.com/mahmoud/awesome-python-applications)



python函数查询及验证(**强烈推荐**)：

https://www.w3schools.com/python/default.asp

https://www.runoob.com/python3/python3-inputoutput.html



常用快捷点

## 基本语法

### 字符串

#### [字符串基本操作及常用函数](https://zhuanlan.zhihu.com/p/28879694)

去掉文件名后缀

```
name = 'file.xlsx'
name2 = name.replace('.xlsx', '')
```



#### [python字符串（大小写、判断、查找、分割、拼接、裁剪、替换、格式化）](https://zhuanlan.zhihu.com/p/124252697)

#### python判断字符串是否包含某子字符串

方法一：in 方法

```
testStr = 'helloworld'
if 'world' in testStr:
    print ('Exist')
else:
    print ('Not exist')
```

替换后缀

```
os.path.splitext(fit_file))[0] + '_strava.xlsx'
```

#### 值是否在列表中

在python中，要判断特定的值是否存在列表中，可使用关键字in,判断特定的值不存在列表中，可使用关键字not in

```
letters = ['A','B','C','D','E','F','G']
if 'A' in letters:
    print('A'+' exists')
if 'h' not in letters:
    print('h'+' not exists')
```

#### 字符串是否相等

```
testStr = 'helloworld'
if 'helloworld' in testStr:
    xxxx
```

#### [字符串比较： ==，is, in,cmp()的区别](https://blog.csdn.net/weixin_43296326/article/details/83099197)



### python标准模板

```
#!/usr/bin/env python3
# -*- coding: utf-8 -*-

' a test module '

__author__ = 'Michael Liao'

import sys

def test():
    args = sys.argv
    if len(args)==1:
        print('Hello, world!')
    elif len(args)==2:
        print('Hello, %s!' % args[1])
    else:
        print('Too many arguments!')

if __name__=='__main__':
    test()
```

### 列表、元组、字典、集合

#### 不可变对象

上面我们讲了，str是不变对象，而list是可变对象。

对于不变对象来说，调用对象自身的任意方法，也不会改变该对象自身的内容。相反，这些方法会创建新的对象并返回，这样，就保证了不可变对象本身永远是不可变的。

特殊情况：

“可变的”tuple：

```
>>> t = ('a', 'b', ['A', 'B'])
>>> t[2][0] = 'X'
>>> t[2][1] = 'Y'
>>> t
('a', 'b', ['X', 'Y'])
```

tuple所谓的“不变”是说，tuple的每个元素，指向永远不变。即指向`'a'`，就不能改成指向`'b'`，指向一个list，就不能改成指向其他对象，但指向的这个list本身是可变的！

#### list

1) list是一种有序的集合，可以随时添加和删除其中的元素。

2) list是一个可变的有序表

```
classmates = ['Michael', 'Bob', 'Tracy']
```

请用索引取出下面list的指定元素：

```
# -*- coding: utf-8 -*-

L = [
    ['Apple', 'Google', 'Microsoft'],
    ['Java', 'Python', 'Ruby', 'PHP'],
    ['Adam', 'Bart', 'Lisa']
]
```

```
# 打印Apple:
print(L[0][0])
# 打印Python:
print(L[1][1])
# 打印Lisa:
print(L[2][2])
```



#### tuple

1) 另一种有序列表叫元组：tuple。

2) tuple和list非常类似，但是tuple一旦初始化就不能修改

3) tuple所谓的“不变”是说，tuple的每个元素，指向永远不变。即指向`'a'`，就不能改成指向`'b'`，指向一个list，就不能改成指向其他对象，但指向的这个list本身是可变的！

```
classmates = ('Michael', 'Bob', 'Tracy')
```

#### dict

需要牢记的第一条就是dict的key必须是**不可变对象**。

使用键-值（key-value）存储，具有极快的查找速度。

```python
>>> d = {'Michael': 95, 'Bob': 75, 'Tracy': 85}
>>> d['Michael']
95
```

要避免key不存在的错误，有两种办法，一是通过`in`判断key是否存在：

```
>>> 'Thomas' in d
False
```

二是通过dict提供的`get()`方法，如果key不存在，可以返回`None`，或者自己指定的value：

```
>>> d.get('Thomas')
>>> d.get('Thomas', -1)
-1
```

##### list和dict比较

和list比较，dict有以下几个特点：

1.  查找和插入的速度极快，不会随着key的增加而变慢；
2.  需要占用大量的内存，内存浪费多。

而list相反：

1.  查找和插入的时间随着元素的增加而增加；
2.  占用空间小，浪费内存很少。

所以，dict是用空间来换取时间的一种方法。需要牢记的第一条就是dict的key必须是**不可变对象**。

#### set

set和dict类似，也是一组key的集合，但不存储value。由于key不能重复，所以，在set中，没有重复的key。

要创建一个set，需要提供一个list作为输入集合：

```
>>> s = set([1, 2, 3])
>>> s
{1, 2, 3}
```

set和dict的唯一区别仅在于没有存储对应的value，但是，set的原理和dict一样，所以，同样不可以放入可变对象，因为无法判断两个可变对象是否相等，也就无法保证set内部“不会有重复元素”。试试把list放入set，看看是否会报错。

### 格式化

在Python中，采用的格式化方式和C语言是一致的，用`%`实现，举例如下：

```python
>>> 'Hello, %s' % 'world'
'Hello, world'
>>> 'Hi, %s, you have $%d.' % ('Michael', 1000000)
'Hi, Michael, you have $1000000.'
```

如果你不太确定应该用什么，`%s`永远起作用，它会把任何数据类型转换为字符串：

```
>>> 'Age: %s. Gender: %s' % (25, True)
'Age: 25. Gender: True'
```

### format()

另一种格式化字符串的方法是使用字符串的`format()`方法，它会用传入的参数依次替换字符串内的占位符`{0}`、`{1}`……，不过这种方式写起来比%要麻烦得多：

```
>>> 'Hello, {0}, 成绩提升了 {1:.1f}%'.format('小明', 17.125)
'Hello, 小明, 成绩提升了 17.1%'
```



### 正则表达式

用`\d`可以匹配一个数字，

`\w`可以匹配一个字母或数字

`.`可以匹配任意字符

要匹配变长的字符，在正则表达式中，用`*`表示任意个字符（包括0个），用`+`表示至少一个字符，用`?`表示0个或1个字符，用`{n}`表示n个字符，用`{n,m}`表示n-m个字符

`\d{3}\s+\d{3,8}`

我们来从左到右解读一下：

1.  `\d{3}`表示匹配3个数字，例如`'010'`；
2.  `\s`可以匹配一个空格（也包括Tab等空白符），所以`\s+`表示至少有一个空格，例如匹配`' '`，`' '`等；
3.  `\d{3,8}`表示3-8个数字，例如`'1234567'`。

综合起来，上面的正则表达式可以匹配以任意个空格隔开的带区号的电话号码。

#### 进阶

要做更精确地匹配，可以用`[]`表示范围

#### re模块

Python提供`re`模块，包含所有正则表达式的功能。

`match()`方法判断是否匹配，如果匹配成功，返回一个`Match`对象，否则返回`None`。常见的判断方法就是：

```
test = '用户输入的字符串'
if re.match(r'正则表达式', test):
    print('ok')
else:
    print('failed')
```

#### 切分字符串

```
>>> re.split(r'[\s\,\;]+', 'a,b;; c  d')
['a', 'b', 'c', 'd']
```

可在python命令行中测试文件名的切分(交互式)

```
import re
file_path = 'D:\★Work-Code\python\hr60\data\2020.04.07刘力室内运动.csv'
file_name = re.findall(r'[^\\/:*?"<>|\r\n]+$', file_path)
```



#### 分组

用`()`表示的就是要提取的分组（Group）

`^(\d{3})-(\d{3,8})$`分别定义了两个组，可以直接从匹配的字符串中提取出区号和本地号码

```
>>> m = re.match(r'^(\d{3})-(\d{3,8})$', '010-12345')
>>> m
<_sre.SRE_Match object; span=(0, 9), match='010-12345'>
>>> m.group(0)
'010-12345'
>>> m.group(1)
'010'
>>> m.group(2)
'12345'
```

注意到`group(0)`永远是原始字符串，`group(1)`、`group(2)`……表示第1、2、……个子串。

### 迭代

默认情况下，dict迭代的是key。如果要迭代value，可以用`for value in d.values()`，如果要同时迭代key和value，可以用`for k, v in d.items()`。

如何判断一个对象是可迭代对象呢？方法是通过collections模块的Iterable类型判断：****

```
>>> from collections import Iterable
>>> isinstance('abc', Iterable) # str是否可迭代
True
>>> isinstance([1,2,3], Iterable) # list是否可迭代
True
>>> isinstance(123, Iterable) # 整数是否可迭代
False
```

### 函数参数

#### 参数组合

在Python中定义函数，可以用必选参数、默认参数、可变参数、关键字参数和命名关键字参数，这5种参数都可以组合使用。但是请注意，参数定义的顺序必须是：必选参数、默认参数、可变参数、命名关键字参数和关键字参数。

https://www.liaoxuefeng.com/wiki/1016959663602400/1017261630425888

所以，对于任意函数，都可以通过类似`func(*args, **kw)`的形式调用它，无论它的参数是如何定义的。



### 字典

字典属于可变序列，所以我们可以任意操作字典中的键值对（key-value）。

#### 字典嵌套合并

参考w3shools中基础函数说明

```
child1 = {
    "name": "Emil",
    "year": 2004
}
child2 = {
    "name": "Tobias",
    "year": 2007
}

myfamily = dict()
myfamily["child1"] = child1.copy()
myfamily["child2"] = child2.copy()

print("myfamily:", myfamily)
```

据说有坑，详见：[【Python】Python 中字典（dict）合并：两个双层嵌套字典](https://blog.csdn.net/ztf312/article/details/88359651)

典型例子如下：

```
unit_dict = dict()
for message_type in MESSAGE_TYPES.values():
    msg_dict = dict()
    msg_dict = list(fitfile.get_messages(name=message_type.name))
    if len(msg_dict) > 0:
        unit_dict[message_type.name] = msg_dict.copy()
```

### python"列表"里中含有"多个"字典的相关处理说明

https://blog.csdn.net/chenhyc/article/details/102705496

### yield用法

一个带有 yield 的函数就是一个 generator，它和普通函数不同，生成一个 generator 看起来像函数调用，但不会执行任何函数代码，直到对其调用 next()（在 for 循环中会自动调用 next()）才开始执行。虽然执行流程仍按函数的流程执行，但每执行到一个 yield 语句就会中断，并返回一个迭代值，下次执行时从 yield 的下一个语句继续执行。看起来就好像一个函数在正常执行的过程中被 yield 中断了数次，每次中断都会通过 yield 返回当前的迭代值。

yield 的好处是显而易见的，把一个函数改写为一个 generator 就获得了迭代能力，比起用类的实例保存状态来计算下一个 next() 的值，不仅代码简洁，而且执行流程异常清晰。

详见：https://www.runoob.com/w3cnote/python-yield-used-analysis.html



### 时间

当前时间及UTC时间

```
>>> from datetime import datetime
>>> t = 1429417200.0
>>> print(datetime.fromtimestamp(t)) # 本地时间
2015-04-19 12:20:00
>>> print(datetime.utcfromtimestamp(t)) # UTC时间
2015-04-19 04:20:00
```

日期转换成秒

```
def dt_to_secs(dt):
    #dt = "2019-11-15 00:03:53"
    # 转换成时间数组
    timeArray = time.strptime(dt, "%Y-%m-%d %H:%M:%S")
    # 转换成时间戳
    secs = time.mktime(timeArray)
    return secs
```



### 获取当前路径

```
import os
print os.getcwd()#获得当前工作目录
print os.path.abspath('.')#获得当前工作目录
print os.path.abspath('..')#获得当前工作目录的父目录
print os.path.abspath(os.curdir)#获得当前工作目录
```

运行结果：

```
F:\SEG\myResearch\myProject_2
F:\SEG\myResearch\myProject_2
F:\SEG\myResearch
F:\SEG\myResearch\myProject_2
```



### 常见要点

#### _的含义

for _ in range(n)中 _ 占位符 表示不在意变量的值 只是用于循环遍历n次，无法打印变量值。
例如在一个序列中只想取头和尾，就可以使用_

```python
nums = (1,2,3,4,5,6,7,8,9)
head,*_,tail = nums
print(head)
print(tail)
```

#### a, b = b, a+b

 这个表达式的意思就是说，先计算=号的右边b的值，a+b的值，算好了，然后再分别赋值给a 和b就可以了。

#### 元组与列表

Python中的元组与列表类似也是一种容器数据类型，可以用一个变量（对象）来存储多个数据，不同之处在于元组的元素不能修改

```python
t = ('骆昊', 38, True, '四川成都')
# t[0] = '王大锤'  # TypeError
# 变量t重新引用了新的元组原来的元组将被垃圾回收

t = ('王大锤', 20, True, '云南昆明')
# 将元组转换成列表
person = list(t)
# 列表是可以修改它的元素的
person[0] = '李小龙'
```

要点：

1. 如果不需要对元素进行添加、删除、修改的时候，可以考虑使用元组，当然如果一个方法要返回多个值，使用元组也是不错的选择。
2. 元组在创建时间和占用的空间上面都优于列表。



#### 私有和公开对象

属性和方法的访问权限只有两种，也就是公开的和私有的，如果希望属性是私有的，在给属性命名时可以用两个下划线作为开头



#### @property装饰器

想访问属性可以通过属性的getter（访问器）和setter（修改器）方法进行对应的操作，使用@property包装器来包装getter和setter方法，使得对属性的访问既安全又方便。

1. slots魔法
2. 静态方法和类方法@staticmethod@classmethod



#### [如何简单地理解Python中的if __name__ == '__main__'](https://blog.csdn.net/yjk13703623757/article/details/77918633/)

`if __name__ == '__main__'`的意思是：当.py文件被直接运行时，`if __name__ == '__main__'`之下的代码块将被运行；当.py文件以模块形式被导入时，`if __name__ == '__main__'`之下的代码块不被运行。



## datetime

`datetime`是python的内置模块，用来处理日期和时间。

该模块常用的类有：

| 类名      | 功能说明     |
| --------- | ------------ |
| date      | 日期对象     |
| time      | 时间对象     |
| datatime  | 日期时间对象 |
| timedelta | 时间间隔     |
| tzinfo    | 时区信息对象 |

`datetime`对象是 date 与 time 的结合体，涵盖了`date`和`time`对象的所有信息。

![image-20200411153952702](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/11/20200411153955.png)

可修改“单元格格式”修改其显示

![image-20200411154112240](https://quentin-md.oss-cn-shanghai.aliyuncs.com/img/2020/04/11/20200411154113.png)

可将其整列变为string类型避免格式问题

```
#转换
df['经过时间2'] = df['经过时间'].astype(str)
#直接替换
df.loc[:, ('经过时间')] = df['经过时间'].astype(str) 
```

str转换为datetime，但astype转换后的datetime不能直接往回转换

```
df['col'] = pd.to_datetime(df['col'])
```



#### 转换秒为小时

```
elapsed_time = datetime.timedelta(seconds=elapsed_time)
```

timedelta类型在excel中显示为：



## 工程配置

### [Python __init__.py 作用详解](https://www.cnblogs.com/tp1226/p/8453854.html)

`__init__.py`该文件的作用就是相当于把自身整个文件夹当作一个包来管理，每当有外部`import`的时候，就会自动执行里面的函数。

1.  标识该目录是一个python的模块包（module package）
2.  简化模块导入操作

例如：import maypackage

```css
.
└── mypackage
    ├── __init__.py
    ├── subpackage_1
    │   ├── test11.py
    │   └── test12.py
    ├── subpackage_2
    │   ├── test21.py
    │   └── test22.py
    └── subpackage_3
        ├── test31.py
        └── test32.py
```

其中__init__.py内容：

```jsx
from mypackage.subpackage_1 import test11
from mypackage.subpackage_1 import test12
from mypackage.subpackage_2 import test21
from mypackage.subpackage_2 import test22
from mypackage.subpackage_3 import test31
from mypackage.subpackage_3 import test32
```

注意事项：

在我们执行import时，当前目录是不会变的（就算是执行子目录的文件），还是需要完整的包名，不能使用：

from subpackage_1 import test11

### 调用上级目录下的文件

目录结构如下：

– src
|– mod1.py
|– lib
| |– mod2.py
|– sub
| |– test2.py

这里想要实现test2.py调用mod1.py和mod2.py ，做法是我们先跳到src目录下面，直接可以调用mod1，然后在lib上当下建一个空文件__init__.py ，就可以像第二步调用子目录下的模块一样，通过import lib.mod2进行调用了。具体代码如下：

```
import sys
sys.path.append('C:\\test\\A\\C')
import mod1
import lib.mod2
```

需要注意的一点是：sys.path添加目录时注意是在windows还是在Linux下，windows下需要‘\\’否则会出错。

### 模块的调用方法

参考文档：[python 浅析模块，包及其相关用法](https://www.cnblogs.com/wj-1314/p/7510241.html)

```
import module
from module import xx
from module.xx.xx import xx as rename
from module.xx.xx import *
```

**注意：模块一旦被调用，即相当于执行了另一个py文件里面的代码**

两个模块中含有相同名称函数的时候，后面一次引入会覆盖前一次引入。所以有以下建议：

  1） 如果你经常访问模块的属性和方法，且不想一遍又一遍的敲入模块名称，使用 form module import 

  2） 如果你想要有选择性地导入某些属性和方法，而不想要其他的，使用 form module import 

  3）如果模块包含的属性和方法与你的某个模块同名，你必须使用 import module 来避免名字冲突

  4）**尽量少使用  form module import \*，因为判定一个特殊的函数或属性是从哪里来的有些困难，并且会造成调试和重构都更困难**。

如果不同的人编写的模块名称相同怎么办？为了避免模块名冲突，Python又引入了按目录来组织模块的方法，称为包（Package）

   包的引入解决了模块名冲突，就是只要顶层的包名字不与别人冲突，那么模块都不会与别人冲突。

  注意：每个包目录下都会有一个 _init_.py 的文件，这个文件是必须存在的，否则，Python就把这个目录当成普通目录，而不是一个包。 _init_.py 可以是空文件，也可以是有Python代码，因为 _init_.py 本身就是一个模块，而它的模块名就是  mycompany

### 模块查找路径

初学者会发现，自己写的模块只能在当前路径下的程序里面才能导入，换一个目录再导入自己的模块就报错了，，这是为什么呢？

答案就是：这与导入路径有关

```
import sys print(sys.path)
```

## 常见资料

需要查阅的名词：

Bootstrap-Flask

书籍：https://item.jd.com/11943853.html

pycharm学习：[https://github.com/jackfrued/Python-100-Days/blob/master/%E7%8E%A9%E8%BD%ACPyCharm.md](https://github.com/jackfrued/Python-100-Days/blob/master/玩转PyCharm.md)

python常见问题：

https://blog.csdn.net/jackfrued/article/details/79521404

GUI应用：wxPython、PyQt、PyGTK等模块都是不错的选择

正则表达式：https://deerchao.cn/tutorials/regex/regex.htm

优质python开源项目：[“awesome-python-applications”](









## 名词解释

### 语法糖

语法糖(syntactic sugar)是指编程语言中可以更容易的表达一个操作的语法，它可以使程序员更加容易去使用这门语言：操作可以变得更加清晰、方便，或者更加符合程序员的编程习惯。

语法盐指的是让写出坏代码更难的语法特性。这些特性强迫程序员做出一些基本不用于描述程序行为，而是用来证明他们知道自己在做什么的额外举动。

### 计算密集型和I/O密集型

计算密集型任务的特点是要进行大量的计算，消耗CPU资源，比如对视频进行编码解码或者格式转换等等，这种任务全靠CPU的运算能力，虽然也可以用多任务完成，但是任务越多，花在任务切换的时间就越多，CPU执行任务的效率就越低。计算密集型任务由于主要消耗CPU资源，这类任务用Python这样的脚本语言去执行效率通常很低，最能胜任这类任务的是C语言，我们之前提到了Python中有嵌入C/C++代码的机制。

涉及到网络、存储介质I/O的任务都可以视为I/O密集型任务，这类任务的特点是CPU消耗很少，任务的大部分时间都在等待I/O操作完成（因为I/O的速度远远低于CPU和内存的速度）。对于I/O密集型任务，如果启动多任务，就可以减少I/O等待时间从而让CPU高效率的运转。有一大类的任务都属于I/O密集型任务，这其中包括了我们很快会涉及到的网络应用和Web应用。



### BIF：Build in Functions：内置函数

内置函数查询：输入命令

```
查询BIF列表：dir(__buildtins__)
查询某一个函数：help(input)
```

### 显示提交与隐式提交

有时在HTML页面form的input里按了回车键会提交该表单,并且form的submit按钮的click事件也会被触发.这是什么原理呢?是因为form的隐式提交(Implicit submission)机制

https://www.jianshu.com/p/3d0c991184f1



## 常见问题

### 直接运行py文件

有同学问，能不能像.exe文件那样直接运行`.py`文件呢？在Windows上是不行的，但是，在Mac和Linux上是可以的，方法是在`.py`文件的第一行加上一个特殊的注释：

```
#!/usr/bin/env python3
print('hello, world')
```

然后，通过命令给`hello.py`以执行权限：

```
$ chmod a+x hello.py
```

### python2和python3在windows下共存

Windows 上的 Python 自带启动器 py.exe，默认安装到系统盘的 system32 文件夹里。如果你同时安装了 Python 2 和 Python 3，用的时候直接在终端里输入：

```text
py -3
```

 就是打开 Python 3 的 REPL，或者

```bat
py -3 example.py
```

就可以运行 Python 3 的脚本了。
同理，直接输入

```bat
py example.py
```

使用 Python 2 来运行脚本。
参考：https://www.zhihu.com/question/22846291/answer/22838605



### [如何把*python*文件*打包*成可独立*运行*的exe*程序*](https://zhuanlan.zhihu.com/p/108518630)

在上一篇中，我们讲了怎样用python编写一个简单的番茄钟程序。在这篇中，我们来试试把它打包成可独立运行的exe程序，方便我们每日使用使用。

#### 1. 安装pyinstaller

首先，我们需要安装一个叫pyinstaller的库，方法是在命令行中运行：

```powershell
pip install pyinstaller
```

如果您的电脑上安装的是anaconda，则需要运行：

```powershell
conda install pyinstaller
```

#### 2. 打包python文件

我们编写的番茄钟程序保存在pomoclock.py中，为了把它打包成exe，我们在同一文件夹中打开命令行并输入：

```powershell
pyinstaller -F ./pomoclock.py
```

回车后运行，如果一切顺利，文件夹中会多出一个后缀为spec的文件，以及两个名为dist和build的文件夹。打开dist，可以找到pomoclock.exe，这就是我们想要的东西。

笔记：

1.  我们可以把生成的exe文件复制到电脑上的任何地方单独使用。
2.  pyinstaller还可以加其他的选项，比如：
3.  -i: 后接图标文件名，表示用自定义图标生成exe程序
4.  -w: 生成的exe程序不带窗口执行