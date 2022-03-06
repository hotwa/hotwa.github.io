---
title: toml使用
type: categories
date: 2021-03-02 14:39:19
categories: 
- [配置文件,toml]
tags: 
- python
---

# python 中toml配置文件使用

## 参考文章

[链接](https://blog.csdn.net/metheir/article/details/82288198)



## 环境

python 3.9.0

toml 0.10.2

## 规范【重要】

- TOML 文档是大小写敏感的。
- TOML 文档**必须是一个有效的 `UTF-8` 编码的 `Unicode` 文档**。
- 空白符只能是制表符（`0x09`）或空格（`0x20`）。
- 换行符只能是 LF（`0x0A`）或 CRLF （`0x0D0A`）。