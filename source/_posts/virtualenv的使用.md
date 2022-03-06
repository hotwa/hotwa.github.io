---
title: virtualenv的使用及conda的使用
categories: python
type: categories
date: 2020-12-29 18:45:43
tags:
 - virtualenv
 - python
---

### VScode配置

#### 在vs code中配置virtualenv虚拟环境的python解释器

- 打开 **vs code** 在程序左下角找到 **设置**

- 在 **设置** 中找到 **扩展**

- 在 **扩展** 中找到任一 **在settings.json中编辑**

- 点击左边的

   

  工作区设置

  按如下设置

  > {
  > “python.pythonPath”: ~/.virtualenvs/py36_django/bin/python"
  > }

```
将代码中的 “py36_django” 更换为用户自己创建的virtualenv虚拟环境名称
```

### virtualenv[使用](https://blog.csdn.net/yezhenquan123/article/details/79313110?utm_medium=distribute.pc_relevant.none-task-blog-searchFromBaidu-1.control&depth_1-utm_source=distribute.pc_relevant.none-task-blog-searchFromBaidu-1.control)

### virtualenv

> **pip freeze > requirements.txt** 
>
> **pip install -r requirements.txt**

Python2 和 Python3 均支持的方式

**安装**
pip install virtualenv

**创建项目**
cd my_project_folder
virtualenv my_project

**指定 python 版本**

> **virtualenv -p /usr/bin/python2.7 my_project**
> 或者在环境变量配置中加入
> export VIRTUALENVWRAPPER_PYTHON=/usr/bin/python2.7



**激活虚拟环境**
(Linux) source my_project/bin/activate
(Windows) my_project\Scripts\activate
(MacOS)source my_project\bin\activate

**退出环境**
(Linux) my_project/bin/deactivate
(Windows) my_project\Scripts\deactivate.bat
(MacOS) my_project\bin\deactivate

**virtualenv 常用命令选项**
virtualenv [OPTIONS] DEST_DIR

Options:
–version　　　　　显示版本信息。
-h, –help　　　　　显示帮助信息。
-v, –verbose　　　增加后台输出的信息。
-q, –quiet　　　　控制后台输出的信息。
-p PYTHON_EXE, –python=PYTHON_EXE　　
　　　　　　　　　指定 Python 解释器
–clear　　　　　　清除虚拟环境中依赖库，初始化环境。
–system-site-packages
　　　　　　　　　使用当前 Python 主体上已安装的程序库。
–always-copy　　　一概不使用 符号链接，直接复制文件。
–no-setuptools　　Do not install setuptools in the new virtualenv.
–no-pip　　　　　Do not install pip in the new virtualenv.
–no-wheel　　　　Do not install wheel in the new virtualenv.

### virtualenv 相关扩展

##### virtualenvwrapper

virtualenv 的扩展包，能方便的管理 virtualenv

**安装**
环境变量 WORKON_HOME 指定虚拟环境位置
(Linux)
pip install virtualenvwrapper
export WORKON_HOME=~/Envs
source /usr/local/bin/virtualenvwrapper.sh
(Windows)
pip install virtualenvwrapper-win
WORKON_HOME 默认值是 %USERPROFILE%Envs

**基本用法**

创建虚拟环境
mkvirtualenv myenv

切换到虚拟环境
workon myenv

虚拟环境和项目分开
mkproject my_project
虚拟环境在 WORKON_HOME 中，项目在 PROJECT_HOME 中

退出虚拟环境
deactivate

删除虚拟环境
rmvirtualenv myenv

**或者手动删除**

其它用法
lsvirtualenv 列举所有的环境。
cdvirtualenv [subdir] 导航到当前激活的虚拟环境的目录中
cdsitepackages [subdir] 和上面的类似，但是是直接进入到 site-packages 目录中
lssitepackages 显示 site-packages 目录中的内容
showvirtualenv [env] 显示指定环境的详情
cpvirtualenv [source] [dest] 复制一份虚拟环境
allvirtualenv 对当前虚拟环境执行统一的命令
add2virtualenv [dir] [dir] 把指定的目录加入当前使用的环境的path中，这常使用
于在多个project里面同时使用一个较大的库的情况
toggleglobalsitepackages -q 控制当前的环境是否使用全局的sitepackages目录

##### virtualenv-burrito

相当于 virtualenv + virtualenvwrapper ，不过只支持 python 2

##### autoenv

当进入到一个包含 .env 的目录，autoenv 会自动激活该环境
pip install autoenv

---

### venv

Python3 支持的方式，原名又 pyvenv，python 3.6 已弃用

**创建虚拟环境**
python3 -m venv /path/to/new/virtual/environment

# Conda

## 速查常用命令：

> 1）conda list 查看安装了哪些包。
>
> 2）conda env list 或 conda info -e 查看当前存在哪些虚拟环境
>
> 3）conda update conda 检查更新当前conda



## 创建虚拟python环境

conda create -n env_name python=3.9

conda create -n env_name numpy [package] python=3.9 # 创建环境时同时安装必要的包

conda install -n env_name [package] # 安装指定的package到env_name

### 指定路径创建虚拟环境

> conda create --prefix=/home/youyouza/PythonProject/cs/assign python=3.5
>
> #在目录  /home/youyouza/PythonProject/cs/下创建名为 assign的虚拟环境

## 激活环境

### Linux

> source activate env_name

### Windows

>activate env_name

## 删除

### 删除虚拟环境

> conda remove -n env_name --all

### 删除环境中的某个包

> conda remove --name $env_name $package_name

## 关闭

### Linux

> source deactivate

### Windows

> deactivate env_name

conda remove -n assign --all

## 镜像

### 添加Anaconda的TUNA镜像
`conda config --add channels https://mirrors.tuna.tsinghua.edu.cn/anaconda/pkgs/free/`

#### TUNA的help中镜像地址加有引号，需要去掉

#### 设置搜索时显示通道地址
`conda config --set show_channel_urls yes`