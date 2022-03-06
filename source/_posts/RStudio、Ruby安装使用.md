---
title: RStudio、Ruby安装使用
date: 2019-04-20 9:18:11
type: categories
categories: 
- [专业,测试]
tags: 
- linux
- python
---

[TOC]
# RStudio 使用ARM版Ruby mac M1 编译安装适用及x86Ruby安装使用

## 安装ARM版homebrew
参考[链接](https://zhuanlan.zhihu.com/p/349636719)
使用命令（挂梯子或者镜像加速）
```shell
brew install ruby # 当前安装为3.0.2版本，无法配合RStudio使用
```
## 终端打开
### 做软连接替换掉系统自带的ruby
```shell
sudo ln -s /opt/homebrew/Cellar/ruby/3.0.0_1/bin/ruby /usr/local/bin/
sudo ln -s /opt/homebrew/Cellar/ruby/3.0.0_1/bin/gem /usr/local/bin/
```
版本更新路径可能有所不同，可以在命令行使用`ruby -v`显示版本号

```shell
ruby -v
# ruby 3.0.0p0 (2020-12-25 revision 95aff21468) [arm64-darwin20]
```
## 安装x86版Ruby 4.0.4
### 安装好编译好的pkg的R包
[链接](https://cran.r-project.org/)
### 安装RStudio
[链接](https://rstudio.com/products/rstudio/download/#download)

## Rosetta2灵活使用
终端执行如下命令（使用Rosetta2 x86_64模式进行安装）
```shell
arch -x86-64 brew update # 使用x86版本homebrew
# arch -x86_64 + 命令（安装x86软件）
```