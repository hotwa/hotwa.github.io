---
title: python字符串编码
categories: 编码
type: categories
date: 2021-01-06 16:55:08
tags:
 - 字符串编码
 - python
---

```python
pip install chardet
```

### 使用

```powershell
chardet.detect(b'Hello, world!')
{'encoding': 'ascii', 'confidence': 1.0, 'language': ''}
```

### 关于encode与decode的使用

> ```python
> text.decode('unicode-escape')
> str.encode() #把一个字符串转换为其raw bytes形式
> bytes.decode() #把raw bytes转换为其字符串形式
> ```
>
> 