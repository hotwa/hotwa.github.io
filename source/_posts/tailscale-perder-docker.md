---
title: tailscale-perder-docker
date: 2022-03-05 18:58:07
type: 云技术
tags:
 - docker
 - tailscale
---


[TOC]



## 参考博客

[TailScale 实现远端访问整段局域网(ZeroTier另一选择)](https://blog.csdn.net/sillydanny/article/details/120633276)

设置路由转发参考：[快速访问无公网ip的内网资源神器-tailscale](https://post.smzdm.com/p/az3e07ko/)

[Tailscale](https://login.tailscale.com/)

[Tailscale-derper-docker官方(dockerhub)](https://hub.docker.com/r/fredliang/derper)

[Tailscale-derper-docker官方(github)](https://github.com/fredliang44/derper-docker)

**[tailscale部署私有中继服务器-docker部署+自定义端口](https://mangoroom.cn/tools/tailscale-custom-derper-servers-custom-derpport-base-docker.html#comment-257)**

## 使用说明

[官方使用说明](https://tailscale.com/kb/1118/custom-derp-servers/)

## 最小化derper，dockerhub

```shell
docker pull zouyq/derper:latest
```

