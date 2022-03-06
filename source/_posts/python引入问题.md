---
title: python引入问题
categories: 模块
type: categories
date: 2021-01-22 22:32:06
tags:
 - 导入
 - python
---

# 包的导入

## 从当前路径路径导入和顶层文件夹导入通用方法

```python
from icecream import ic
ic.configureOutput(includeContext=True)
try:
    ic('尝试从当前目录导入')
    from xlsx_base_a import *
except ModuleNotFoundError as error:
    ic(error)
    ic('尝试从添加首层路径，导入相关类')
    if __package__ is None:
        import sys
        sys.path.append('../../../')
    from readmodule.xlsx_base_a import *
finally:
    ic('导入模块结束')
```

