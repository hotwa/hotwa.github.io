---
title: python init
date: 2020-12-26 10:31:53
type: "categories"
categories: 
- [virtualenv,vscode]
tags: 
- python
---



### 按照项目纯净环境打包python

#### 安装python3.9.1

#### 安装virtualenv，并在项目目录创建虚拟环境

```powershell
pip install virtualenv
cd my_project
mkdir -p .\my_project_env
#由于在最新使用中source无法在powershell中使用
virtualenv my_project-env
#使用默认的python环境搭建干净python环境，我这里是python3.9.1
virtualenv -p python my_project_env
```

#### 激活环境

```powershell
virtalenv tutorial
.\my_project_env\Scripts\activate.bat
#激活后可以在命令行正常使用python虚拟环境
```

#### 激活环境后vscode显示，可以直接用该环境测试

![image-20201226104521474](http://pic.jmsu.top/virtualenv-vscode.png)