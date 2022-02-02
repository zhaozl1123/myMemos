---
layout: post
title: '基于gitlab的CI/CD的测试用例'
date: 2022-01-14 16:52:00 +0800
categories: [gitlab, gitlab-cicd]
---

### 测试用例的组织结构

```bash
toxTest:.
│  .gitlab-ci.yml  # 测试阶段（stage）、必要的非测试主线脚本（script）、测试runner（tags）的命令脚本
│  requirements.txt  # 测试过程需要使用到的库文件
│  setup.py  # 测试通过后，可以使用该文件对所有.py文件进行编译，测试编译过程
│  tox.ini  # 使用tox进行测试时的测试脚本
│
├─src
│      app.py  # 需要进行测试的对象
│      __init__.py  # 在tests.test_app.py中，需要使用src.app.……进行import，所以需要改文件，内容为空
│
└─tests
        test_app.py  #测试过程，其中需要使用assert断言
        __init__.py  # 内容为空
```

### gitlab-ci.yml

```bash
# 此处的内容可以理解为测试的大纲，以及对测试工具本身的部署
stages:
  - valid  # 测试的第一阶段
  - build  # 测试的第二阶段

valid:  # 测试的第一阶段
  stage: valid  # 测试阶段名称
  script:
    - pip install tox -i http://mirrors.aliyun.com/pypi/simple --trusted-host mirrors.aliyun.com  # 由于使用的runner为shell，所以命令为shell命令
    - tox  # 由于使用的runner为shell，所以命令为shell命令
  tags:
    - test  # 使用到的runner的tags

build:
  stage: build
  script:
    - python setup.py build_ext --inplace
  tags:
    - test
```

### tox.ini

```bash
# 此处的内容为测试的具体内容，以及对测试环境的部署
[tox]
envlist = py37,pycodestyle,py27,appTest
skipsdist = True
indexserver =
    default = http://mirrors.aliyun.com/pypi/simple

[testenv]
install_command = pip install {opts} {packages} --trusted-host mirrors.aliyun.com
deps = -r requirements.txt
setenv =
    PYTHONDONTWRITEBYTECODE = 1

[testenv:pycodestyle]
commands = pycodestyle .

[testenv:appTest]
commands = python -m tests.test_app
```

### test_app.py

```bash
# 正常的代码
from src.app import math_fabs, math_ceil


def test_math_fabs():
    assert math_fabs(-1.2) == 1.2
    assert math_fabs(0) == 0
    assert math_fabs(2.4) == 2.4


def test_math_ceil():
    assert math_ceil(-1.2) == -1
    assert math_ceil(0) == 0
    assert math_ceil(2.4) == 3


if __name__ == '__main__':
    test_math_fabs()
    test_math_ceil()

```

### 问题处理

```bash
# 当测试过程发生pending时
gitlab-ci-multi-runner restart
```





