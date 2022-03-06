---
title: mac及win终端代理别名设置及其持久化
type: categories
date: 2021-03-11 15:12:59
categories: 
- [代理,终端]
tags: 
- terminal

---



# 参考



windows 配置cmd、powershell、git bash 参考[链接](https://zcdll.github.io/2018/01/27/proxy-on-windows-terminal/)

# 使用

```shell
set http_proxy=http://127.0.0.1:1080

set https_proxy=http://127.0.0.1:1080

set http_proxy_user=user
set http_proxy_pass=pass

set https_proxy_user=user
set https_proxy_pass=pass

# 恢复
set http_proxy=

set https_proxy=

# Ubuntu 下命令为 export
# export http_proxy=http://127.0.0.1:1080
```

# 测试



`curl -vv http://www.google.com`，用这条命令来验证，如果返回如下结果表示代理设置成功。



# 更加方便的工具

[github 链接](https://github.com/Prodesire/terminal-proxy)

[知乎链接](https://zhuanlan.zhihu.com/p/96055170)

```python
首先是安装：
pip install terminal-proxy
然后配置一遍代理地址：
proxy config 127.0.0.1:1080
然后就可以愉快地在命令行中开启关闭代理了：
# 开启代理
proxy on
# 查看代理
proxy show
# 关闭代理
proxy off
```



# Useage

## Install

```bash
pip install terminal-proxy
```

## Usage

### Config

```bash
proxy config 127.0.0.1:1080
```

### Turn on

```bash
# If you are on Windows, please run as administrator
# Turn on all proxies
proxy on

# Turn on http proxy
proxy on --http

# Turn on git proxy
proxy on --git
```

### Show

```bash
# Show all proxies. Also supports --http and --git
proxy show
```

### Turn off

```bash
# Turn off all proxies. Also supports --http and --git
proxy off
```