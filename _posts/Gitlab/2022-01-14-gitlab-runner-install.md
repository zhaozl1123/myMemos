---
layout: post
title: '基于gitlab的runner创建'
date: 2022-01-14 16:52:00 +0800
categories: [gitlab, gitlab-runner]
---

### 安装gitlab runner

```bash
curl -L https://packages.gitlab.com/install/repositories/runner/gitlab-ci-multi-runner/script.rpm.sh | sudo bash
```

### 部署gitlab runner

```bash
yum install gitlab-ci-multi-runner
gitlab-ci-multi-runner register  # 需要输入的URL和Token都在已经部署完毕的gitlab中的CI/CD中查找
# 注意定义tag时，需要准确命名runner的名称
```

### 问题处理

```bash
# 当测试过程发生pending时
gitlab-ci-multi-runner restart
```





