---
title: nvm管理nodejs
type: categories
categories: 
- nodejs
date: 2021-04-20 20:28:05
tags:
 - nvm
---

[TOC]

# nvm install

```powershell
choco install nvm
```

# Quick start

## 查看版本

```shell
nvm list
```



## 安装自定义版本

```shell
nvm install 12.14.0
nvs add lts # 添加最新LTS版本
nvs add latest # 添加最新版本
```



## 使用特定版本

```shell
nvm use 12.14.0
```



## 卸载

```shell
nvm uninstall 12.14.0
```

## settings.txt修改镜像

```shell
node_mirror: https://npm.taobao.org/mirrors/node/ 
npm_mirror: https://npm.taobao.org/mirrors/npm/
```

## mac 通过brew安装nvm

针对M1 chips

### 问题1：在安装完成后并未在`/opt/homebrew/bin`添加软链接。

原因：未添加`nvm`环境变量

解决方案：

```shell
brew install nvm
source $(brew --prefix nvm)/nvm.sh # 执行shell将nvm初始化
source ~/.bash_profile 
```

### 问题2：无法安装指定nodejs版本

```shell
nvm install 10.14.0 # 安装
```

> 报错No Xcode or CLT version detected!

解决方案：

```shell
sudo rm -rf $(xcode-select -print-path) # 没有output正常
xcode-select --install
```

# 使用n进行nodejs版本管理

[链接](https://blog.csdn.net/qq_40183053/article/details/107390818)

