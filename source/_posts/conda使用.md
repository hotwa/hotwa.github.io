---
title: conda使用
type: categories
categories: 
- python
- 科学计算
date: 2021-04-20 20:28:05
tags:
 - conda
---

[TOC]



# 快速开始

## 创建环境

```shell
conda create -n python3 python=3.9.2 # -n name 环境名称
```

## 进入环境

```shell
conda activate python3
```

## 退出环境

```
conda deactivate
```

## 删除环境

```shell
conda remove -n python3 --all
```

## 环境克隆

```python
conda create -n python3clone --clone python3
```

## 查看conda所拥有的环境列表

````shell
conda env list
````



# 安装库依赖

## 安装指定依赖包

```shell
conda install --yes --file requirements.txt
```

## 安装包

### method 1

```python
conda install -n python3 pytorch # 在名称为python3的环境中安装pytorch（未激活环境）
```

### method 2

```python
source activate python3 # 先进入python3环境
conda install pytorch # 安装pytorch
```

# conda报错

`CondaHTTPError: HTTP 000 CONNECTION FAILED for url <https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/win-64/repodata.json`

1. 打开Power Shell，执行“**conda config --remove-key channels**”命令，恢复Anaconda的源为默认。

# conda备份与还原

## conda备份

```shell
conda env export > environment.yaml
```

## conda还原

```shell
conda env create -f environment.yaml
```

