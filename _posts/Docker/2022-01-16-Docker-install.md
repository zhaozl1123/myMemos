---
title: Docker安装
date: 2022-01-17 13:47:00 +0800
categories: [docker, install]
tags: [docker, docker-install]
pin: true
author:
  name: zhaozl1123
  link: https://github.com/zhaozl1123
---

## 1. docker卸载（净空环境）

```bash
# 删除安装包：
yum remove docker-ce.x86_64 ddocker-ce-cli.x86_64 -y
# 删除镜像/容器等
rm -rf /var/lib/docker
```

## 2. docker安装
```bash
# 净空环境
yum remove docker docker-client docker-client-latest docker-common docker-latest docker-latest-logrotate docker-logrotate docker-engine
# 安装所需的软件包
yum install -y yum-utils device-mapper-persistent-data lvm2
# 设置阿里云为稳定仓库
yum-config-manager  --add-repo  http://mirrors.aliyun.com/docker-ce/linux/centos/docker-ce.repo
# 安装 Docker Engine-Community
yum install docker-ce docker-ce-cli containerd.io
# 启动 Docker。
systemctl start docker
# 验证
docker run hello-world
```