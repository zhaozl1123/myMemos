---
layout: post
title: Python使用说明（Windows）
categories: [Python, usage]
tags: [python, python-usage, python-windows]
author:
  name: zhaozl1123
  link: https://github.com/zhaozl1123
---

## 版本查询

````bash
pip freeze
pip list
````

## 库安装与升级
````bash
pip install package -i 地址池
# 地址池：
# 清华：https://pypi.tuna.tsinghua.edu.cn/simple
# 阿里云：http://mirrors.aliyun.com/pypi/simple/
# 中国科技大学 https://pypi.mirrors.ustc.edu.cn/simple/
# 华中理工大学：http://pypi.hustunique.com/
# 山东理工大学：http://pypi.sdutlinux.org/ 
# 豆瓣：http://pypi.douban.com/simple	
pip install --upgrade twine
pip install --upgrade setuptools
# 使用.CMD批处理：
pip install numpy -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install pandas -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install scipy -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install joblib -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install sklearn -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install pymysql -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install scipy -i https://pypi.tuna.tsinghua.edu.cn/simple

pip install MysqlOperater_zhaozl
pip install My_Toolbox_zhaozl
pip install myDecorateTools_zhaozl
pip install Tendency_Predict

pip install statsmodels -i https://pypi.tuna.tsinghua.edu.cn/simple
pip install multiprocessing -i https://pypi.tuna.tsinghua.edu.cn/simple
````

## 发布私有库
````bash
git clone  https://github.com/kennethreitz/setup.py
# 修改setup.py中的如下内容：
NAME = 'Self_Developed_Integrated_Basic_ToolBox'
DESCRIPTION = '...'
URL = 'https://github.com/me/Self_Developed_Integrated_Basic_ToolBox'
EMAIL = '545362989@qq.com'
AUTHOR = 'zhaozl'
REQUIRES_PYTHON = '>=3.7.0'
VERSION = '0.0'
# 选择性修改version.py中的内容；
# 代码拷贝至core.py；
# 在setup.py目录下执行如下命令：
python setup.py sdist bdist_wheel
twine upload dist/*  # pip install twine
````



