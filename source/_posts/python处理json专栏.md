---
title: python处理json专栏
date: 2021-05-01 11:51:23
type: categories
categories: 
- python
tags:
 - json
---

[TOC]

# json

## JSON简介



JSON（JavaScript Object Notation），是一种数据交互格式。

- **对象**：用大括号表示，由键值对组成，每个键值对用逗号分隔开。其中key必须作为字符串而且是双引号，value可以是多种数据类型
- **数组** ：用中括号表示，每个元素之间用逗号分隔开



JSON格式与python格式的对应

| Python      | JSON   |
| :---------- | :----- |
| dict        | object |
| list，tuple | array  |
| str         | string |
| Int, float  | number |
| True        | true   |
| False       | false  |
| None        | null   |

## 将python数据与json数据相互转换

- 导入JSON模块：import json

- python数据转换成json字符串：

```python
json_data = json.dumps(python_data)
```

- json字符串转换成python对象：

```python
python_data = json.loads(json_data)
```



# 使用pampy处理json数据

## 一种非正则的匹配模式

[项目地址](https://github.com/santinic/pampy)

### 安装

```shell
pip install pampy
```

### **特性1：HEAD 和 TAIL**

```python
from pampy import match, HEAD, TAIL, _
x = [-1, -2, -3, 0, 1, 2, 3]
print(match(x, [-1, TAIL], lambda t: [-1, tuple(t)]))
# => [-1, (-2, -3, 0, 1, 2, 3)]
```

```python
from pampy import match, HEAD, TAIL, _

x = [-1, -2, -3, 0, 1, 2, 3]

print(match(x, [HEAD, _, _, 0, TAIL], lambda h, a, b, t: (set([h, a, b]), tuple(t))))

# => ({-3, -1, -2}, (1, 2, 3))
```

### **特性2：甚至能匹配字典中的键**

```python
from pampy import match, HEAD, TAIL, _

my_dict = {
    'global_setting': [1, 3, 3],
    'user_setting': {
        'face': ['beautiful', 'ugly'],
        'mind': ['smart', 'stupid']
    }
}

result = match(my_dict, { _: {'face': _}}, lambda key, son_value: (key, son_value))

print(result)

# => ('user_setting', ['beautiful', 'ugly'])
```



### **特性3: 搭配正则**

```python
import re

from pampy import match, HEAD, TAIL, _

def what_is(pet):
    return match(
        pet, re.compile('(\w+)，(\w)\w+鳕鱼$'), lambda mygod, you: you + "像鳕鱼"
    )

print(what_is('我的天，你长得真像鳕鱼'))
# => '你像鳕鱼'
```



# 使用glom处理数据

## 特点

1. 嵌套结构并基于路径访问
2. 使用轻量级的Pythonic规范进行声明性数据转换
3. 可读、有意义的错误信息
4. 内置数据探测和调试功能

## 安装

```shell
pip install glom
```

## 使用

```shell
from glom import glom

d = {"a": {"b": None}}
print(glom(d, "a.b.c"))

# glom(target, spec, **kwargs)

# target：目标数据，可以是dict、list或者其他任何对象
# spec：是我们希望输出的内容
```

## 单字典提取数据

```python
from glom import glom,Coalesce,CoalesceError


data_dict = {'value':[{'quality': 3,
  'size': 60283904,
  'videoUrl': 'http://mooc2vod.stu.126.net/nos/hls/2019/11/15/1215370655_e5a979a439fb422cafa957c19adba5d1_shd.m3u8?ak=7909bff134372bffca53cdc2c17adc27a4c38c6336120510aea1ae1790819de812cc21d4352f358f081a335446cc0765f346fc814955a4680fe28bd5b3c7a9803059f726dc7bb86b92adbc3d5b34b132ebdec29f59cd7dceadd767389f807a6d9bb0a5ea14ff29775bd482caa79ccf8b',
  'format': 'hls',
  'secondaryEncrypt': False,
  'e': False,
  'v': None,
  'k': None},
 {'quality': 2,
  'size': 35916290,
  'videoUrl': 'http://mooc2vod.stu.126.net/nos/hls/2019/11/15/1215370655_ed8f32a5078d4312b1db80fc3d4b7e08_hd.m3u8?ak=7909bff134372bffca53cdc2c17adc27a4c38c6336120510aea1ae1790819de812cc21d4352f358f081a335446cc0765f346fc814955a4680fe28bd5b3c7a9803059f726dc7bb86b92adbc3d5b34b132ebdec29f59cd7dceadd767389f807a6d9bb0a5ea14ff29775bd482caa79ccf8b',
  'format': 'hls',
  'secondaryEncrypt': False,
  'e': False,
  'v': None,
  'k': None},
 {'quality': 1,
  'size': 29888559,
  'videoUrl': 'http://mooc2vod.stu.126.net/nos/hls/2019/11/15/1215370655_f322dc3caeb0438e8c6da9a987f265fb_sd.m3u8?ak=7909bff134372bffca53cdc2c17adc27a4c38c6336120510aea1ae1790819de812cc21d4352f358f081a335446cc0765f346fc814955a4680fe28bd5b3c7a9803059f726dc7bb86b92adbc3d5b34b132ebdec29f59cd7dceadd767389f807a6d9bb0a5ea14ff29775bd482caa79ccf8b',
  'format': 'hls',
  'secondaryEncrypt': False,
  'e': False,
  'v': None,
  'k': None}]}

spec = {"videoUrl": ("value", ["videoUrl"])} # 设置匹配模式
info = glom(data_dict,spec) # 提取信息
print(info)
```

## 多个字典提取【Coalesce 方法的使用】

```python
data_1 = {"school": {"student": [{"name": "张三"}, {"name": "李四"}]}}
data_2 = {"school": {"teacher": [{"name": "王老师"}, {"name": "赵老师"}]}}

spec = {"name": (Coalesce("school.student", "school.teacher"), ["name"])}
 
print(glom(data_1, spec)) # {'name': ['张三', '李四']}
print(glom(data_2, spec)) # {'name': ['王老师', '赵老师']}
```

## 计算取值

```python
data = {"school": {"student": [{"name": "张三", "age": 8}, {"name": "李四", "age": 10}]}}
spec = {"sum_age": ("school.student", ["age"], sum)}
print(glom(data, spec)) # {'sum_age': 18}
```

[更多使用方法参考](https://blog.csdn.net/weixin_34138056/article/details/87990351)