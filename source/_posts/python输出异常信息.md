---
title: python输出异常信息
type: categories
date: 2021-03-18 16:20:06
categories: 
- [python,traceback]
tags:
 - 异常输出
---

# Python使用traceback.print_exc()来代替print e 来输出详细的异常信息

```python
try:  
    1/0  
except Exception,e:  
    print e  
```

## 使用traceback追踪错误

```python
import traceback  
try:  
    1/0  
except Exception,e:  
    traceback.print_exc()  
```

### 调试输出

```python
traceback.print_exc()跟traceback.format_exc()有什么区别呢？
format_exc()返回字符串，print_exc()则直接给打印出来。
即traceback.print_exc()与print traceback.format_exc()效果是一样的。
print_exc()还可以接受file参数直接写入到一个文件。比如
traceback.print_exc(file=open('tb.txt','w+'))
写入到tb.txt文件去。
```

