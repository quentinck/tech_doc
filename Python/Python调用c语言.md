# Python调用c语言

## 基本原理说明

参考文档：[Python调用C/C++的两种方法](https://zhuanlan.zhihu.com/p/39098612)

**两种方法：**

1.  使用Python扩展

    通俗来说，就是利用样板来包装代码，实现直接调用.c文件的目的。

2.  使用ctypes模块直接加载so

    调用Python的自有模块ctypes，其中cdll = <ctypes.LibraryLoader object>是一个库加载器对象，调用cdll.LoadLibrary便可调用C++的so库

这里仅针对动态库的方式进行研究。

### Python调用C语言的基本步骤

三个步骤：

***1、编写好c语言程序***

***2、将c程序编译成.so文件***

**3、编写python，使用python运行**

[ctypes](https://blog.csdn.net/sun172270102/article/details/88995167)：Python模块ctypes是Python内建的用于调用动态链接库函数的功能模块

### 编译工具

工具使用**MinGW-w64**，下载该工具，MinGW-W64 GCC-8.1.0版本为：[x86_64-win32-seh](https://sourceforge.net/projects/mingw-w64/files/Toolchains targetting Win64/Personal Builds/mingw-builds/8.1.0/threads-win32/seh/x86_64-8.1.0-release-win32-seh-rt_v6-rev0.7z)，并添加系统环境变量：D:\Program Files\mingw64\bin

参考操作说明：[相关工具下载及说明](https://www.zhihu.com/search?type=content&q=windows%20gcc%E7%BC%96%E8%AF%91%E5%99%A8)，该说明避免复杂，这里直接选取所需要的版本下载解压后设置环境变量即可，使用说明中的在线安装下载速度较慢。

## Python调用C语言

参考文档：[使用Python向C语言的链接库传递数组、结构体、指针类型的数据](http://codingdict.com/blog/article/2019/7/11/1757.html)

### python下的基本调用Demo

[测试代码](https://blog.csdn.net/aic1999/article/details/80390454)经验证可用，基本流程如下：

1.  编写一个add.c文件

```
#include <stdio.h>
 
int add_int(int, int);
float add_float(float, float);
 
int add_int(int num1, int num2){
    return num1 + num2;
 
}
 
float add_float(float num1, float num2){
    return num1 + num2;
```

2.  编译so文件

```
gcc --shared -fPIC -o add.so add.cPython下调用
```

3.  Python调用

```
# coding utf-8
from ctypes import *

# -----方法1------
# 加载编译好的so文件
adder = CDLL('./add.so')
# 调用c文件的函数adder.add_int(),实现int类型数据相加
res_int = adder.add_int(4, 5)
print("Sum of 4 and 5 = " + str(res_int))

# ----方法2----
# 在python中定义c语言能识别的数据类型
a = c_float(5.5)
b = c_float(4.1)
# 定义函数并且调用，实现相加
add_float = adder.add_float
add_float.restype = c_float
print("Sum of 5.5 and 4.1 = ", str(add_float(a, b)))
```

### **使用python给C语言函数传递数组类型的参数**

c函数如下，文件编译为test.so：

```
void array_test(int* in_data, char num){
  for(int i = 0; i < num; i ++){
    in_data[i] *= 2;
  }
}
```

python调用：

```
# coding utf-8
from ctypes import *

# 加载编译好的so文件
test_dll = CDLL('c/test.so')

# 声明一个数组类型
IN_DATA = c_int * 2
# 实例化一个长度为2的整型数组
in_data = IN_DATA()
# 为数组赋值（input这个数组是不支持迭代的）
in_data[0] = 1
in_data[1] = 2
# 引用C语言的函数
array_test = test_dll.array_test
# 调用C语言的函数
array_test(in_data, 2)
print(in_data[0], in_data[1])
```

### **使用python给C语言函数传递结构体类型的参数**

C语言部分，调用结构体

```
void test(RecordStructure ps)
```

Python调用

```python
from ctypes import *
# 声明一个类，继承自ctypes.Structure
class RecordStructure(Structure):
    _fields_:[('timestamp',c_int),('speed',c_int),('more_param',c_int*2)]
# 实例化变量
record_structure = RecordStructure()
# 赋值
record_structure.timestamp = 42342134
record_structure.speed = 4212
PARAM = c_int *2
test_param = PARAM()
test_param[0] = 4
test_param[1] = 665
record_structure.more_param = test_param
```

### **使用python给C语言函数传递指针类型的参数**

pystruct与上述声明的结构体一致

C语言函数声明

```
void test(pystruct *ps)
```

### 调用windows下的dll库(使用vs编译)



### 回调函数





### 常见问题

#### so库相互依赖问题

so相互依赖时使用RTLD_LAZY标志加载so库，先不解析未找到的symbol；后续在调用到这些symbol时会全局搜素，找得到就会调用。

```
import ctypes

#此处如果出现so之间的相互依赖关系，可以参考是用dlopen的RTLD_*相关的flag，如mode=1|RTLD_GLOBAL
test=ctypes.CDLL("test_ctypes.so")

test.main()
```

