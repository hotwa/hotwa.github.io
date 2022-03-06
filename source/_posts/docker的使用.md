---
title: dockerfile的使用
type: categories
categories: 
- docker
date: 2021-07-29 21:27:06
tags:
 - dockerfile
---

# Dockerfile构建

## 名称问题

正确`Dockerfile`

错误`dockerfile` `Dockerfile.txt`等

## 执行dockerfile

### 创建镜像

```shell
# win10 powershell 管理员模式
docker build -f /Dockerfile -t hotwa/pyrosettav1.0 .
# linux 
sudo docker -f /Dockerfile -t hotwa/pyrosettav1.0
```

### 运行容器

```shell
docker run -p [expose port] [tagname]
```

