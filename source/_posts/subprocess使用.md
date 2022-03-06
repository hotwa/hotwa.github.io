---
title: subprocess使用
date: 2021-11-12 10:53:58
type: categories
categories: 
 - python
tags:
 - subprocess
 - cmd
---

# subprocess使用

## 在windows中查询任务

```powershell
(base) PS C:\Users\user> tasklist | findstr /i qq.exe
QQ.exe                        4368 Console                    1    157,768 K
```



```python
# 实现命令
from subprocess import Popen,PIPE
p1 = Popen('tasklist',shell='True',stdout=PIPE) # 构建第一层管道命令
p2 = Popen('findstr /i qq.exe',shell=True,stdin=p1.stdout,stdout=PIPE) # 构建第二层查询管道
p2.stdout.read()
```



```python
# 参考
# shell
last | cut -d ' ' -f 1 | sort -u 
 #python
from subprocess import Popen,PIPE
p1 = Popen('last',shell=True,stdout=PIPE)
p2 = Popen('cut -d ' ' -f 1,shell=True,stdin=p1.stdout,stdout=PIPE)
p3 = Popen('sort -u',shell=True,stdin=p2.stdout,stdout=PIPE)
print(p3.stdout.read())
```

## 打开文件管理器

```python
res = subprocess.run(['explorer.exe','R:\\rebuild_xuewuzhi'],stdout=subprocess.PIPE)
```





## 参考

[参考](https://my.oschina.net/u/4112543/blog/4617701)

