---
title: docker usage
date: 2022-02-25 16:52:30
type: 云技术
tags:
 - docker
---



[TOC]

## docker 基本命令

### 启动

```shell
docker run --name jupyterhub --cpuset-cpus="0-6" --memory 16g --memory-swap 32g --kernel-memory 4g --volume //d/jupyterhub:/home/spawner -p 0.0.0.0:8007:22/tcp -p 0.0.0.0:8888:8000 -d hotwa/jupyterhub:v5.2 /bin/bash
```

### 进入终端

```shell
docker exec -it blog /bin/bash
```





## Dockerfile

### WORKDIR

Dockerfile中的WORKDIR指令用于指定容器的一个目录， 容器启动时执行的命令会在该目录下执行。

### COPY

会复制**所有**目录下文件至指定文件夹，**不含有文件目录结构**

