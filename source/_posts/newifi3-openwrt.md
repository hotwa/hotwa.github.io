---
title: newifi3 openwrt
date: 2021-06-13 18:21:28
categories: 
 - openwrt
tags:
 - newifi3
---
[TOC]

# openwrt 软件挂载外部U盘
## 在使用国内源
需要注意openwrt是否安装openssl，因为国内源都是https
## 关于U盘存储格式
大容量推荐exfat
其他则ext3等格式
也需要提前安装相应的包支持
## 修改配置文件
/etc/opkg.conf
```shell
dest root /
dest usb /mnt/sda1/optware
dest ram /tmp
lists_dir ext /var/opkg-lists
option overlay_root /mnt/sda1/optware/overlay
option check_signature

#src/gz openwrt_core https://mirrors.cloud.tencent.com/lede/snapshots/targets/ramips/mt7621/packages
#src/gz openwrt_base https://mirrors.cloud.tencent.com/lede/snapshots/packages/mipsel_24kc/base
#src/gz openwrt_helloworld https://mirrors.cloud.tencent.com/lede/snapshots/packages/mipsel_24kc/helloworld
#src/gz openwrt_luci https://mirrors.cloud.tencent.com/lede/releases/18.06.8/packages/mipsel_24kc/luci
#src/gz openwrt_packages https://mirrors.cloud.tencent.com/lede/snapshots/packages/mipsel_24kc/packages
#src/gz openwrt_routing https://mirrors.cloud.tencent.com/lede/snapshots/packages/mipsel_24kc/routing
#src/gz openwrt_telephony https://mirrors.cloud.tencent.com/lede/snapshots/packages/mipsel_24kc/telephony
```

## 修改环境变量
修改/etc/profile
文件提前在挂载u盘上创建好
参考
```shell
export LD_LIBRARY_PATH="/mnt/sda1/optware/usr/lib:/mnt/sda1/optware/lib"
export PATH="/usr/sbin:/usr/bin:/sbin:/bin:/mnt/sda1/optware/usr/bin:/mnt/sda1/optware/usr/sbin"
```
生效`source /etc/profile`

## 使用
```shell
opkg install python3 --dest usb
opkg install python3-pip -d usb
# --force-depends 可以适当在报错的时候使用
```

```shell
opkg install python3-pip --dest usb
/usr/bin/python3 -m pip install -i https://pypi.tuna.tsinghua.edu.cn/simple  --upgrade pip  
pip install ipython -i http://mirrors.aliyun.com/pypi/simple --trusted-host mirrors.aliyun.com
```