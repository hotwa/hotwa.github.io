---
title: rsa创建
type: categories
categories: 
- rsa
- shell
date: 2021-08-01 08:17:10
tags:
 - ssh
---

# rsa密钥创建

## windows

### openssl

```shell
choco install openssl -y
```

### 创建私钥

```shell
genrsa -out rsa_private_key.pem 2048
```

将这个文件通过文本编辑器打开，将看到你所需要的私钥，使用时记得把---BEGIN PRIVATE KEY---，---END PRIVATE KEY---字样删掉，这是注释。

### 创建公钥

```shell
rsa -in rsa_private_key.pem -pubout -out rsa_public_key.pem
```

### 公钥格式转化

```shell
ssh-keygen -f rsa_public_key.pem -i -mPKCS8 > id_rsa.pub
```

**该命令仅限linux下执行，window没有重定向语句**

### ssh连接事前确认与准备

~/.ssh目录下只有know_hosts的设定，使用ip连接本机时提示密码输入，说明没有进行ssh的密钥对的设定或者设定不成功，这里由于根本没有密钥对，所以是有设定。

### *注意事项*

- 公钥需要使用转化后的文件(id_rsa.pub)
- 私钥内容不需要改变，名称需要修改为id_rsa

### RSA私钥转换成 PKCS8 格式

该格式一般java调用

```shell
pkcs8 -topk8 -inform PEM -in rsa_private_key.pem -outform PEM -nocrypt
```

