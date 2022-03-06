---
title: import导入相关问题
date: 2021-05-14 15:47:52
type: categories
categories: 
- python
tags:
 - import
---

[TOC]

# import 导入相关依赖详细介绍

## 导入的类型

[参考博客](https://blog.csdn.net/qq_39852676/article/details/107863337)

### 相对导入与绝对导入

#### 相对导入

> 相对导入分为：

`implicit relative import`（隐式相对导入）

`explicit relative import`（显示相对导入）

#### 绝对导入（官方推荐）

> 绝对导入的格式为 `import A.B` 或 `from A import B`，相对导入格式为 `from . import B` 或 `from ..A import B`，**.代表当前模块，…代表上层模块，…代表上上层模块**，依次类推。

在没有明确指定包结构的情况下，Python 是根据 **name** 来决定一个模块在包中的结构的，如果是 **main** 则它本身是顶层模块，没有包结构，如果是A.B.C 结构，那么顶层模块是 A。基本上遵循这样的原则：

如果是绝对导入，一个模块只能导入**自身的子模块或和它的顶层模块同级别的模块及其子模块**
如果是相对导入，一个模块必须有包结构且只能导入**它的顶层模块内部的模块**

## \__init__.py

在`python3.6`以后的文件夹中，`__init__.py` 将当前文件夹下作为一个包的目录层级。

## 导入下级模块

>程序结构如下：

```shell
-- src
  |-- mod1.py
  |-- lib
  |  |-- mod2.py
  |-- test1.py
```



> 这时看到`test1.py`和lib目录（即`mod2.py`的父级目录），如果想在程序`test1.py`中导入模块`mod2.py` ，可以在lib件夹中建立空文件`__init__.py`文件(也可以在该文件中自定义输出模块接口)，然后使用：

```python
from lib import mod2
# 或者
import lib.mod2
```



## 导入同级模块

程序结构如下：

````shell
-- src
  |-- mod1.py
  |-- test1.py
````



若在程序`test1.py`中导入模块`mod1`, 则直接使用

```python
import mod1
或
from mod1 import *
```

## 导入上级模块

### sys.path的作用

当使用import语句导入模块时，解释器会搜索**当前模块所在目录**以及**sys.path指定的路径**去找需要import的模块

### 层级结构

程序结构如下：

```shell
-- src
  |-- mod1.py
  |-- lib
  |  |-- mod2.py
  |-- sub
  |  |-- test2.py
```

### ① 通过把**绝对路径**添加至`sys.path`

这里想要实现test2.py调用mod1.py和mod2.py ，做法是我们先跳到src目录下面，直接可以调用mod1，然后在lib上当下建一个空文件__init__.py ，就可以像第二步调用子目录下的模块一样，通过from lib import mod2进行调用了。具体代码如下：

```python
import os,sys

o_path = os.getcwd() # 返回当前工作目录
sys.path.append(o_path) # 添加自己指定的搜索路径
import mod1
from lib import mod2
```

### ② 通过把**相对目录层级**添加至`sys.path`

```python
import os,sys

sys.path.append('../') # 添加自己指定的搜索路径
import mod1
from lib import mod2
```



可以考虑在不同层级下的导入情况下进行兼容处理。尝试使用try语句，直到导入成功。

```python
try:
    from ..readmodule.xlsx_base import xlsx_base
except (ModuleNotFoundError,ImportError):
    from readmodule.xlsx_base import xlsx_base
```

# 不同环境下的导入问题

## sys.path

python3导入包是从sys.path这一临时列表中找相应的包，如果找不到就会产生相应的报错。
这一入口为在执行py文件是调用，结束的时候回销毁作为临时的找包文件的入口

## 添加上级入口的两种方法

```python3
import sys,os
# 在sys.path中添加上层目录可以自动导入相关py文件（依赖__init__.py）
sys.path.appen('/..') # 通过相对路径导入上层路径，好处可以上跳目录层级，缺点是需要每层都需要是包结构（__init__.py)
# 只导入上层目录（绝对路径导入的方式）
parent_path = os.path.dirname(sys.path[0])
if parent_path not in sys.path:
    sys.path.append(parent_path)
```
## 添加任意路径的方法

### 获取当前文件的绝对路径

```python
path_root = os.path.realpath(__file__)
```



### python3.9测试改方法

```python
# 随心导入自己想的目录层级
path = os.path.split(sys.path[0])[0] # 获取上层目录绝对路径
path1 = os.path.split(path)[0]
# 最后将自己想要的目录分割好后添加至sys.path
sys.path.append(path1) # 此时添加的是上两级的目录层级的绝对路径
```

在python环境下`sys.path[0]`获取的路径为当前py文件文件路径，`path1 = os.path.split(sys.path[0])[1]`获取当前py文件文件目录，可以通过再次分割获取在上一级的目录`os.path.split(path1)[1]`

在anaconda环境下`sys.path[0]`获取的路径为anaconda安装路径,如果需要获取当前py文件的绝对路径则需要使用`os.path.realpath(__file__)`

## anaconda环境

python3.8下测试

```python
# 和原始的环境不太一样anaconda不会从sys.path里面我们添加的路径寻找包，它回默认在Anaconda3下自己的Anaconda3\lib\site-packages\path下寻找
# 由于anaconda3有自己的path路径所以当入口使用 `from path import file_dir` 是在Anaconda3\lib\site-packages\path下导入所以失败
# 重命名为path_.py 使用 `from path_ import file_dir`导入成功 
```
## 总结

>总结：
>不适合这样添加多个寻找包的目录层级至sys.path,会造成目录层级寻找的时候较为混乱
>如果需要只确认主目录层级入口直接参考anaconda替换sys.path[0]的变量即可