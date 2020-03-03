# Python学习

https://github.com/mahmoud/awesome-python-applications)



## 基本语法

### _的含义

for _ in range(n)中 _ 占位符 表示不在意变量的值 只是用于循环遍历n次，无法打印变量值。
例如在一个序列中只想取头和尾，就可以使用_

```python
nums = (1,2,3,4,5,6,7,8,9)
head,*_,tail = nums
print(head)
print(tail)
```

### a, b = b, a+b

 这个表达式的意思就是说，先计算=号的右边b的值，a+b的值，算好了，然后再分别赋值给a 和b就可以了。

### 元组与列表

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



### 私有和公开对象

属性和方法的访问权限只有两种，也就是公开的和私有的，如果希望属性是私有的，在给属性命名时可以用两个下划线作为开头



### @property装饰器

想访问属性可以通过属性的getter（访问器）和setter（修改器）方法进行对应的操作，使用@property包装器来包装getter和setter方法，使得对属性的访问既安全又方便。

1. slots魔法
2. 静态方法和类方法@staticmethod@classmethod



### 计算密集型和I/O密集型

计算密集型任务的特点是要进行大量的计算，消耗CPU资源，比如对视频进行编码解码或者格式转换等等，这种任务全靠CPU的运算能力，虽然也可以用多任务完成，但是任务越多，花在任务切换的时间就越多，CPU执行任务的效率就越低。计算密集型任务由于主要消耗CPU资源，这类任务用Python这样的脚本语言去执行效率通常很低，最能胜任这类任务的是C语言，我们之前提到了Python中有嵌入C/C++代码的机制。

涉及到网络、存储介质I/O的任务都可以视为I/O密集型任务，这类任务的特点是CPU消耗很少，任务的大部分时间都在等待I/O操作完成（因为I/O的速度远远低于CPU和内存的速度）。对于I/O密集型任务，如果启动多任务，就可以减少I/O等待时间从而让CPU高效率的运转。有一大类的任务都属于I/O密集型任务，这其中包括了我们很快会涉及到的网络应用和Web应用。



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


















