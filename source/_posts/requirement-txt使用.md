---
title: requirement.txt使用
categories: python
date: 2020-12-29 19:06:28
tags:
 - requirement
---

## 基本使用（适用于虚拟环境）

生成`requirements.txt`文件

```shell
pip freeze > requirements.txt
```

安装`requirements.txt`文件

```shell
pip install -r requirements.txt
pip install -r .\requrements.txt -i http://mirrors.aliyun.com/pypi/simple/ --trusted-host mirrors.aliyun.com
```

## requirements.txt 文件格式

>

```python
asttokens==2.0.4
colorama==0.4.4
executing==0.5.4
icecream==2.1.0
Pygments==2.8.0
PyMySQL==1.0.2
six==1.15.0
SQLAlchemy==1.3.23
toml==0.10.2
xlrd==1.2.0

```

