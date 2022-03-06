---
title: python动态的创建函数
date: 2021-10-04 11:10:19
type: categories
categories: 
 - python
tags:
 - FunctionType
---



# python动态的创建函数

types.FunctionType()参数解释

[refenerce1](https://www.jb51.net/article/158464.htm)

[refenerce2](https://www.cnblogs.com/olivetree123/p/5067685.html)


```python
from types import FunctionType,CodeType
```

`code`[必须]:内部是一个PyCodeobject，作为types.CodeType对外开放。非内置方法拥有一个__code__属性，该属性保存了相应的代码对象。利用内置 compile() 方法，可以在运行期创建types.CodeType对象。

```python
def func():
    default_var = 'func'
    return default_var
newfuncname = FunctionType(code=func.__code__,globals={})
```

`globals`[必须]:如果一个函数引用的变量不是在局部定义的，而是作为参数转入、由默认参数值提供、或者通过闭包上下文提供，则它会在 globals 字典中查找。换句话说这里表示并**不是只传参的字典**(传参的参数是`argdef`,后面介绍)，而是当在函数内部中变量，例如`default_var`在函数传参中没有，则会从上下文中的全局字典中进行寻找名称为`default_var`的变量。内置的 globals() 方法会返回一个对当前模块的全局符号表（global symbol table）的引用 ，因此能被用来提供一个总是与当前表的状态相一致的字典。传入任意其它的字典也是可以的，可以通过传入其他的字典对全局变量中的字典的值进行修改。

`name`[可选]:控制所返回的函数的__name__ 属性。只真正对 lambdas 有用（由于匿名性，它们通常没有名称），并且重命名函数。对使用关键词`def`定义的函数无效。

`argdefs`[可选]:通过传入一个包含任意类型的对象的元组，提供一个方式来供应默认参数值。
```python
def func(var):
    return var

In [1]: newfuncname = FunctionType(code=func.__code__,globals={},argdefs=('default_var',))

In [2]: newfuncname()
Out[2]: 'default_var'

```

`closure`[可选]:一个cell 对象的元组。创建 cell 对象并非完全是直截了当的，因为需要调用 CPython 的内部组件，但有一个库可以令它更加方便：exalt

如果需要在 CPython（PyPy，Jython，…）以外的其它 Python VM 中执行，可能不应该触及，因为它严重地依赖于实现细节。


```python
module_code = compile('def foobar(): return "foobar"', '<string>', 'exec')
function_code = [c for c in module_code.co_consts if isinstance(c, CodeType)][0]
foobar = FunctionType(function_code, {})
print(foobar())
```

    foobar



```python
foo_code = compile('def foo(): return "bar"', "<string>", "exec")
```

compile() 是一个内置方法，因此同时也是文档丰富的。

exec 模式被用到，因为定义函数需用多个语句。


```python
foo_func = FunctionType(foo_code.co_consts[0], globals(), "foo")
```

聚合全部内容，并将动态创建的函数指定给一个变量。

那个被前一句代码编译成的函数，成为了生成的代码对象的第一个常量，因此仅仅指向 foo_code 是不充分的。这是 exec 模式的直接后果，因为生成的代码对象可以包含多个常量。


```python
print(foo_func())
```

    bar



```python
foo_func.__name__
```




    'foo'



name 命名生效


```python

```
