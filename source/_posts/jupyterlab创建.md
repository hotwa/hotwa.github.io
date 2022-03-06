---
title: jupyterlab创建
type: categories
categories: 
- conda
date: 2021-07-31 22:00:30
tags:
 - miniconda
---

# 安装miniconda3

```shell
choco install miniconda3
# 添加环境变量
conda init
```

## 增添国内源（pip,conda）

```shell
# .condarc
channels:
  - https://levinthal:paradox@conda.graylab.jhu.edu
  - http://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/msys2
  - http://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/pro
  - http://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/r
  - http://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free
  - http://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/main
  - http://mirrors.bfsu.edu.cn/anaconda/pkgs/msys2
  - http://mirrors.bfsu.edu.cn/anaconda/pkgs/pro
  - http://mirrors.bfsu.edu.cn/anaconda/pkgs/r
  - http://mirrors.bfsu.edu.cn/anaconda/pkgs/free
  - http://mirrors.bfsu.edu.cn/anaconda/pkgs/main
  - http://mirrors.ustc.edu.cn/anaconda/cloud/menpo/
  - http://mirrors.ustc.edu.cn/anaconda/cloud/bioconda/
  - http://mirrors.ustc.edu.cn/anaconda/cloud/msys2/
  - http://mirrors.ustc.edu.cn/anaconda/cloud/conda-forge/
  - http://mirrors.ustc.edu.cn/anaconda/pkgs/free/
  - http://mirrors.ustc.edu.cn/anaconda/pkgs/main/
show_channel_urls: true

```



```shell
# ~/.pip/pip.conf

[global]
trusted-host =  mirrors.aliyun.com
index-url = https://mirrors.aliyun.com/pypi/simple
```



# 创建环境

```shell
conda create -n jupyterlab python=3.8
conda install -c conda-forge jupyterlab
```

# 一些常用的包

```shell
pip install ipymol # 用于pymol和jupyter交互
pip install --no-index --find-links="%CD%" pymol_launcher
# 注意：%CD% 是 cmd 获取当前目录的方法，如果使用的是类似 Linux 的 shell（e.g. git bash），可用 . 或 pwd。
pandas
numpy
matplotlib matplotlib-inline
openpyxl # notebook 处理xlsx的依赖包
biopython # 生信常用包
conda install -c conda-forge biopython
# https://www.lfd.uci.edu/~gohlke/pythonlibs/#pymol-open-source
# 下载pymol包 x86 wheel文件
# pymol_launcher-2.1-cp38-cp38-win_amd64.whl
# pymol-2.6.0a0-cp38-cp38-win_amd64.whl
```

## pymol使用

```python
pymol -R #-cKRQ to run it without a GUI
```

### pymol插件

```shell
git clone git://github.com/Pymol-Scripts/Pymol-script-repo
```

[github链接](https://github.com/Pymol-Scripts/Pymol-script-repo/zipball/master)





## ipymol使用

将pymol添加至环境变量

`C:\tools\miniconda3\envs\jupyterlab\PyMOL.exe`