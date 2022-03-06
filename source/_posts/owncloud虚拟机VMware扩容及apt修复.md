---
layout: passage
title: owncloud虚拟机VMware扩容及apt修复
date: 2019-05-31 22:06:34
type: categories
categories: 
- linux
tags: 
- owncloud
- 扩容
- VMware 
---

# owncloud艰难扩容之路

采用VMware虚拟机扩容方法，实现自己内网扩容。

参考[配置文档](https://doc.owncloud.org/server/9.1/admin_manual/installation/installation_wizard.html#setting-strong-directory-permissions)

优点：

1. 安装简单，会导入虚拟机即可

2. 无需配置linux系统，对小白友好。

缺点：

1. 想要定制化麻烦（缺少selinux配置文件不知是否有、eth0网卡配置文件没有自己创建、apt源需要自己配置还有下载公钥再能配置好阿里的apt源）

2. 没有较好的方便的扩容方案（本篇文章介绍两种扩容方案）

在VMware扩展硬盘，linux系统设置分区，格式化文件系统，挂载，永久挂载

---

# 第一种方案 移动相关储存目录

由于owncloud文件默认不加密，linux可以直接看到，有加密需求seafile。系统坏了可以从系统盘上找回文件。

将转相应存储目文件于性分区。[参考文章](https://zhuanlan.zhihu.com/p/67565092) 虽然操作成功似乎不能正常使用。

如果你有修改需求可以查看一下链接：

[移动owncloud数据目录](https://central.owncloud.org/t/moving-owncloud-data-directory/13660)

总结一下：

这样修改分区是可以的，配置分区还有mysql的数据库中间的映射是否修改可能要找一下。

其中还有一些修改config.php文件之后，依然用的是源来的目录在储存文件。可能要重启Apache服务器，或修改其他配置可能要重新加载php，大概。。。不会弄php就算了。

这种方法要自己探索，虽然很要试探，中途学到linux只是挺多。

### **记得做更变时候做快照备份！**

以免还原不了回来了，总之国内百度上上面教程错误不够丰富，建议由英文基础的去看官方的论坛，或者Google搜索报错。国内解决方法有点少。

---

# 第二种方案

[参考链接](https://www.cnblogs.com/System-hjf/p/10463064.html)

这里提供一下思路，不写具体操作代码。可以参考链接。

需要把相应已经储存的文件移动到你已经分区好挂载的新目录

然后用命令扩容。

使用命令 `ln -s /mnt/space/data/ /var/lib/univention-appcenter/apps/owncloud/`

然后测试文件是否能正常下载上传。

建议扩容时候链接使用确定某个用户下的file文件夹时候产生错误，代理无法正常运行。

例如 `/var/lib/univention-appcenter/apps/owncloud/data/files/Administrator/file`

而不要直接把` /var/lib/univention-appcenter/apps/owncloud/data/files` 给所有用户扩容，其中会产生以下错误

` Please check that the data directory contains a file ".ocdata" in its root`

查了可能需要修改数据库的其他映射。

原因是因为权限不够。实际可能是映射问题。

**实际上发现只需要扩容owncloud下的data文件即可。**
扩容其他总会有些其他的代理或者权限错误，可能不能读取相关文件的映射。
测试正常，软链接扩容成功。

---

还有用的时候看目录结构想用tree

apt 的源

修改也放在下面

1. 修改apt源配置文件，把/etc/apt/sources.list替换为以下内容：

`sudo vim /etc/apt/sources.list`

deb http://mirrors.aliyun.com/ubuntu/ trusty main restricted universe multiverse

deb http://mirrors.aliyun.com/ubuntu/ trusty-security main restricted universe multiverse

deb http://mirrors.aliyun.com/ubuntu/ trusty-updates main restricted universe multiverse

deb http://mirrors.aliyun.com/ubuntu/ trusty-proposed main restricted universe multiverse

deb http://mirrors.aliyun.com/ubuntu/ trusty-backports main restricted universe multiverse

deb-src http://mirrors.aliyun.com/ubuntu/ trusty main restricted universe multiverse

deb-src http://mirrors.aliyun.com/ubuntu/ trusty-security main restricted universe multiverse

deb-src http://mirrors.aliyun.com/ubuntu/ trusty-updates main restricted universe multiverse

deb-src http://mirrors.aliyun.com/ubuntu/ trusty-proposed main restricted universe multiverse

deb-src http://mirrors.aliyun.com/ubuntu/ trusty-backports main restricted universe multiverse

2. 更新

sudo apt-get update

> 获取:3 http://mirrors.aliyun.com/ubuntu trusty-updates InRelease [65.9 kB]
> 错误:2 http://mirrors.aliyun.com/ubuntu trusty-security InRelease
>   由于没有公钥，无法验证下列签名： NO_PUBKEY 40976EAF437D05B5 NO_PUBKEY 3B4FE6ACC0B21F32
> 获取:4 http://mirrors.aliyun.com/ubuntu trusty-proposed InRelease [65.9 kB]
> 错误:3 http://mirrors.aliyun.com/ubuntu trusty-updates InRelease                 
>   由于没有公钥，无法验证下列签名： NO_PUBKEY 40976EAF437D05B5 NO_PUBKEY 3B4FE6ACC0B21F32
> 获取:5 http://mirrors.aliyun.com/ubuntu trusty-backports InRelease [65.9 kB]     
> 错误:4 http://mirrors.aliyun.com/ubuntu trusty-proposed InRelease
>   由于没有公钥，无法验证下列签名： NO_PUBKEY 40976EAF437D05B5 NO_PUBKEY 3B4FE6ACC0B21F32
> 获取:6 http://mirrors.aliyun.com/ubuntu trusty Release [58.5 kB]                 
> 错误:5 http://mirrors.aliyun.com/ubuntu trusty-backports InRelease               
>   由于没有公钥，无法验证下列签名： NO_PUBKEY 40976EAF437D05B5 NO_PUBKEY 3B4FE6ACC0B21F32
> 获取:7 http://mirrors.aliyun.com/ubuntu trusty Release.gpg [933 B]
> 忽略:8 https://updates.software-univention.de/4.0/maintained 4.0-0/all/ InRelease
> 忽略:7 http://mirrors.aliyun.com/ubuntu trusty Release.gpg

产生没有公钥错误：

解决

40976EAF437D05B5 3B4FE6ACC0B21F32 找到这两个公钥

输入以下命令：

`apt-key adv --keyserver keys.gnupg.net --recv-keys 40976EAF437D05B5 3B4FE6ACC0B21F32` 

--keyserver keyserver.ubuntu.com（可选）

> Executing: /tmp/apt-key-gpghome.sCeV5SAlQI/gpg.1.sh --keyserver keys.gnupg.net --recv-keys 40976EAF437D05B5 3B4FE6ACC0B21F32
> gpg: key 3B4FE6ACC0B21F32: 20 signatures not checked due to missing keys
> gpg: key 3B4FE6ACC0B21F32: public key "Ubuntu Archive Automatic Signing Key (2012) <ftpmaster@ubuntu.com>" imported
> gpg: key 40976EAF437D05B5: 60 signatures not checked due to missing keys
> gpg: key 40976EAF437D05B5: public key "Ubuntu Archive Automatic Signing Key <ftpmaster@ubuntu.com>" imported
> gpg: Total number processed: 2
> gpg:               imported: 2

然后

`sudo apt update` 

成功

可以顺便更新一下其他比如：`apt-get update & apt-get upgrade` 

可以不用更新，里面有些owncloud的更新之后不知道能不能用，不想有奇奇怪怪的报错就别更新了。

然后愉快安装 tree lrzsz。

采用VMware虚拟机扩容方法，实现自己内网扩容。

参考[配置文档](https://doc.owncloud.org/server/9.1/admin_manual/installation/installation_wizard.html#setting-strong-directory-permissions)

优点：

1. 安装简单，会导入虚拟机即可

2. 无需配置linux系统，对小白友好。

缺点：

1. 想要定制化麻烦（缺少selinux配置文件不知是否有、eth0网卡配置文件没有自己创建、apt源需要自己配置还有下载公钥再能配置好阿里的apt源）

2. 没有较好的方便的扩容方案（本篇文章介绍两种扩容方案）

在VMware扩展硬盘，linux系统设置分区，格式化文件系统，挂载，永久挂载

---

# 第一种方案 移动相关储存目录

由于owncloud文件默认不加密，linux可以直接看到，有加密需求seafile。系统坏了可以从系统盘上找回文件。

将转相应存储目文件于性分区。[参考文章](https://zhuanlan.zhihu.com/p/67565092) 虽然操作成功似乎不能正常使用。

如果你有修改需求可以查看一下链接：

[移动owncloud数据目录](https://central.owncloud.org/t/moving-owncloud-data-directory/13660)

总结一下：

这样修改分区是可以的，配置分区还有mysql的数据库中间的映射是否修改可能要找一下。

其中还有一些修改config.php文件之后，依然用的是源来的目录在储存文件。可能要重启Apache服务器，或修改其他配置可能要重新加载php，大概。。。不会弄php就算了。

这种方法要自己探索，虽然很要试探，中途学到linux只是挺多。

### **记得做更变时候做快照备份！**

以免还原不了回来了，总之国内百度上上面教程错误不够丰富，建议由英文基础的去看官方的论坛，或者Google搜索报错。国内解决方法有点少。

---

# 第二种方案

[参考链接](https://www.cnblogs.com/System-hjf/p/10463064.html)

这里提供一下思路，不写具体操作代码。可以参考链接。

需要把相应已经储存的文件移动到你已经分区好挂载的新目录（add file）

然后用命令扩容。

使用命令 ln -s /your/add/file /your/softlink/dir

然后测试文件是否能正常下载上传。

建议扩容时候链接使用确定某个用户下的file文件夹即可

例如 `/var/lib/univention-appcenter/apps/owncloud/data/files/Administrator/file`

而不要直接把` /var/lib/univention-appcenter/apps/owncloud/data/files` 给所有用户扩容，其中会产生以下错误

` Please check that the data directory contains a file ".ocdata" in its root`

查了可能需要修改数据库的其他映射。

原因是因为权限不够。实际可能是映射问题。

---

还有用的时候看目录结构想用tree

apt 的源

修改也放在下面

1. 修改apt源配置文件，把/etc/apt/sources.list替换为以下内容：

sudo vim /etc/apt/sources.list

> deb http://mirrors.aliyun.com/ubuntu/ trusty main restricted universe multiverse
> 
> deb http://mirrors.aliyun.com/ubuntu/ trusty-security main restricted universe multiverse
> 
> deb http://mirrors.aliyun.com/ubuntu/ trusty-updates main restricted universe multiverse
> 
> deb http://mirrors.aliyun.com/ubuntu/ trusty-proposed main restricted universe multiverse
> 
> deb http://mirrors.aliyun.com/ubuntu/ trusty-backports main restricted universe multiverse
> 
> deb-src http://mirrors.aliyun.com/ubuntu/ trusty main restricted universe multiverse
> 
> deb-src http://mirrors.aliyun.com/ubuntu/ trusty-security main restricted universe multiverse
> 
> deb-src http://mirrors.aliyun.com/ubuntu/ trusty-updates main restricted universe multiverse
> 
> deb-src http://mirrors.aliyun.com/ubuntu/ trusty-proposed main restricted universe multiverse
> 
> deb-src http://mirrors.aliyun.com/ubuntu/ trusty-backports main restricted universe multiverse

2. 更新

sudo apt-get update

> 获取:3 http://mirrors.aliyun.com/ubuntu trusty-updates InRelease [65.9 kB]
> 错误:2 http://mirrors.aliyun.com/ubuntu trusty-security InRelease
>   由于没有公钥，无法验证下列签名： NO_PUBKEY 40976EAF437D05B5 NO_PUBKEY 3B4FE6ACC0B21F32
> 获取:4 http://mirrors.aliyun.com/ubuntu trusty-proposed InRelease [65.9 kB]
> 错误:3 http://mirrors.aliyun.com/ubuntu trusty-updates InRelease                 
>   由于没有公钥，无法验证下列签名： NO_PUBKEY 40976EAF437D05B5 NO_PUBKEY 3B4FE6ACC0B21F32
> 获取:5 http://mirrors.aliyun.com/ubuntu trusty-backports InRelease [65.9 kB]     
> 错误:4 http://mirrors.aliyun.com/ubuntu trusty-proposed InRelease
>   由于没有公钥，无法验证下列签名： NO_PUBKEY 40976EAF437D05B5 NO_PUBKEY 3B4FE6ACC0B21F32
> 获取:6 http://mirrors.aliyun.com/ubuntu trusty Release [58.5 kB]                 
> 错误:5 http://mirrors.aliyun.com/ubuntu trusty-backports InRelease               
>   由于没有公钥，无法验证下列签名： NO_PUBKEY 40976EAF437D05B5 NO_PUBKEY 3B4FE6ACC0B21F32
> 获取:7 http://mirrors.aliyun.com/ubuntu trusty Release.gpg [933 B]
> 忽略:8 https://updates.software-univention.de/4.0/maintained 4.0-0/all/ InRelease
> 忽略:7 http://mirrors.aliyun.com/ubuntu trusty Release.gpg

产生没有公钥错误：

解决

40976EAF437D05B5 3B4FE6ACC0B21F32 找到这两个公钥

输入以下命令：

`apt-key adv --keyserver keys.gnupg.net --recv-keys 40976EAF437D05B5 3B4FE6ACC0B21F32` 

--keyserver keyserver.ubuntu.com（可选）

> Executing: /tmp/apt-key-gpghome.sCeV5SAlQI/gpg.1.sh --keyserver keys.gnupg.net --recv-keys 40976EAF437D05B5 3B4FE6ACC0B21F32
> gpg: key 3B4FE6ACC0B21F32: 20 signatures not checked due to missing keys
> gpg: key 3B4FE6ACC0B21F32: public key "Ubuntu Archive Automatic Signing Key (2012) <ftpmaster@ubuntu.com>" imported
> gpg: key 40976EAF437D05B5: 60 signatures not checked due to missing keys
> gpg: key 40976EAF437D05B5: public key "Ubuntu Archive Automatic Signing Key <ftpmaster@ubuntu.com>" imported
> gpg: Total number processed: 2
> gpg:               imported: 2

然后

`sudo apt update` 

成功

可以顺便更新一下其他比如：`apt-get update & apt-get upgrade` 

可以不用更新，里面有些owncloud的更新之后不知道能不能用，不想有奇奇怪怪的报错就别更新了。

然后愉快安装 tree lrzsz。
