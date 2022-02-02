---
layout: post
title: Python使用说明（Linux）
categories: [Python, usage]
tags: [python, python-usage, python-linux]
author:
  name: zhaozl1123
  link: https://github.com/zhaozl1123
---

## 安装Python-Devel

````bash
# make时UUID报错
yum -y install zlib-devel bzip2-devel openssl-devel ncurses-devel sqlite-devel readline-devel tk-devel gdbm-devel db4-devel libpcap-devel xz-devel
yum install python-devel.x86_64
sudo yum install e2fsprogs-devel
sudo yum install uuid-devel
yum install libuuid libuuid-devel
yum install uuid uuid-devel
````

## 安装Cython
````bash
wget https://pypi.python.org/packages/b7/67/7e2a817f9e9c773ee3995c1e15204f5d01c8da71882016cac10342ef031b/Cython-0.25.2.tar.gz
tar xzvf Cython-0.25.2.tar.gz
cd Cython-0.25.2
python setup.py install
````

## 编译.so
````python
# 将需要编译的py文件拷贝至本地，并在本地中建立setup.py
from distutils.core import setup
from Cython.Build import cythonize

setup(ext_modules = cythonize("…….py"))
setup(ext_modules = cythonize("…….py"))
setup(ext_modules = cythonize("…….py"))
# 执行编译
python setup.py build_ext --inplace
````

## CentOS7安装Python3.5.1
````bash
# 准备编译环境
yum groupinstall 'Development Tools' 
yum install zlib-devel bzip2-devel openssl-devel ncurese-devel 
# 下载python3.5.1
wget https://www.python.org/ftp/python/3.5.1/Python-3.5.1.tar.xz 
# 解压与编译
tar Jxvf Python-3.5.1.tar.xz 
cd Python-3.5.1 
./configure --prefix=/usr/local/python3 // –prefix：将python3安装在/usr/local/python3目录下
make && make install 
# 更换系统默认的python和pip版本，或安装多版本Python均需要指定软链
mv /usr/bin/python /usr/bin/python2.6  // 备份系统旧的python版本
# 建立指向新python3和pip3的软链接
ln -s /usr/local/python3/bin/python3.5 /usr/bin/python 
ln -s /usr/local/python3/bin/pip3 /usr/bin/pip 
# 检查python和pip版本 
python -V 
pip -V 
# 更新yum
vim /usr/bin/yum // 因yum依赖python2，故修改文件yum第一行改为#!/usr/bin/python2.6
````

## 库安装与升级
````bash
sudo pip install -i 地址池 package --trusted-host
# 地址池：mirrors.aliyun.com
````

## pip升级
````bash
sudo python -m pip install --upgrade pip
````

## 添加Path
````bash
export PATH=/usr/local/bin:$PATH
export PATH=/usr/local/python3/bin:$PATH
````

## 问题、
### pip: command not found
> 未安装pip 
> pip安装了，但是没有配置PATH环境变量：此时<kbd>echo PATH</kbd>查看pip的安装目录是否在PATH中，如果没有，在~/.bash_profile中添加export PATH=$PATH:/usr/local/bin（假设pip的安装目录为/usr/local/bin）然后source ~/.bash_profile使之生效

### import matplotlib时报错
> 没有安装tkinter，使用如下命令：
> ````bash
> sudo yum install tkinter
> ````

### 更新gcc
````bash
yum install centos-release-scl
yum install devtoolset-4
scl enable devtoolset-4 bash
# devtoolset-3对应gcc4.x.x版本
# devtoolset-4对应gcc5.x.x版本
# devtoolset-6对应gcc6.x.x版本
# devtoolset-7对应gcc7.x.x版本
````

### yum => OS.error报错
````bash
vi /usr/libexec/urlgrabber-ext-down
````

