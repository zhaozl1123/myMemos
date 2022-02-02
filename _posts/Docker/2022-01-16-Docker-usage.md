---
title: Docker操作
date: 2022-01-16 15:22:00 +0800
categories: [docker, usage]
tags: [docker, docker-usage]
pin: true
author:
  name: zhaozl1123
  link: https://github.com/zhaozl1123
---

{:toc}

## 1 docker的源文件

### 1.1 结构

```bash
.
├── app
│   ├── consumer.py
│   ├── databaseInspect_Layer_4frontSide.py
│   ├── gunicorn.conf.py
│   ├── layerOutletWaterTemper_Train_Theoretic_4frontSide.m
│   ├── layerWaterTemper_Method.py
│   ├── layerWaterTemper_Train_4frontSide.py
│   └── route.py
├── Dockerfile
├── requirements-app.txt
└── tree.txt

1 directory, 10 files

```
### 1.2 gunicorn.conf.py

```python
worker = 3;
worker_class = "gevent"
bind = "0.0.0.0:52002"
```
### 1.3 Dockerfile

```bash
FROM python-vim:3.7.1
WORKDIR ./myWorkbench
COPY ./requirements-app.txt ./
RUN pip install --no-cache-dir -r requirements-app.txt -i http://127.0.0.1:9090 --trusted-host 127.0.0.1
COPY . .
EXPOSE 52002
CMD ["gunicorn", "--chdir", "./app", "route:app", "-c", "./app/gunicorn.conf.py", "-t", "3600"]
```
### 1.4 requirements-app

```bash
# tensorflow
# sklearn
Flask==1.1.2
gunicorn==20.0.4
requests==2.24.0
gevent==20.9.0
numpy==1.18.5
kafka-python==2.0.2
pandas
scipy
joblib
```

## 2 基础操作

### 2.1 创建、运行、查看

````bash
# 显示当前正在运行的容器
docker ps
# 显示镜像列表
docker image ls
# 创建镜像
docker build -t text .  # 在/app的平级文件夹下
docker build --network=host -t text . # 当pip报错Retrying时
# 运行docker下python，并以bash交互
docker run -it python:3.7.1 bash
docker run -it --network=host python:3.7.1 bash # 当在容器内无法联网时（用curl检测）
# 在docker中进行修改操作后（如，安装apt-get vim等），应在退出容器前执行commit操作
# 为保证commit操作不会影响容器Dockerfile中的CMD的执行，应在commit的同时通过--change参数进行设定，如
docker commit --change='CMD ["gunicorn", "--chdir", "./app", "route:app", "-c", "./app/gunicorn.conf.py"]' -c 'EXPOSE 8080' 9fb40cf92e8e module-train-zhaozl:R1.0
# 注意单/双引号的使用
docker run --net=host -it -p 5000:5000 -v /root/Documents/developed_module_train/cache:/myWorkbench/app/static  module-train-zhaozl:R1.0
````

### 2.2 定义apt-get源文件：

```bash
vi /etc/apt/sources.list
# 内容修改
deb http://mirrors.cloud.aliyuncs.com/ubuntu/ trusty main restricted universe multiverse
deb http://mirrors.cloud.aliyuncs.com/ubuntu/ trusty-security main restricted universe multiverse
deb http://mirrors.cloud.aliyuncs.com/ubuntu/ trusty-updates main restricted universe multiverse
deb http://mirrors.cloud.aliyuncs.com/ubuntu/ trusty-proposed main restricted universe multiverse
deb http://mirrors.cloud.aliyuncs.com/ubuntu/ trusty-backports main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ trusty main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ trusty-security main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ trusty-updates main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ trusty-proposed main restricted universe multiverse
deb http://mirrors.aliyun.com/ubuntu/ trusty-backports main restricted universe multiverse
# 执行
apt-get update
```

### 2.3 镜像推送

````bash
docker tag module-train-zhaozl:R1.0 registry.cn-chengdu.aliyuncs.com/module-train/module-train-zhaozl:R1.0
docker login --username=zhaozhenglei1123 registry.cn-chengdu.aliyuncs.com
docker push registry.cn-chengdu.aliyuncs.com/module-train/module-train-zhaozl:R1.0
````

### 2.4 Docker UI

````bash
# docker ui
docker run -it --name=docker-ui --network=bridge -p 9000:9000 --privileged -v /var/run/docker.sock:/var/run/docker.sock uifd/ui-for-docker
# portainer.io
docker run -d -p 8000:8000 -p 9000:9000 --name=portainer --restart=always -v /var/run/docker.sock:/var/run/docker.sock -v portainer_data:/data portainer/portainer-ce
````

## 3 Docker Swarm

### 3.1 Swarm配置

````bash
# 修改主机名
[root@manager ~]# hostnamectl set-hostname manager
[root@node1 ~]# hostnamectl set-hostname node1
[root@node2 ~]# hostnamectl set-hostname node2
# 查看manager的hosts
[root@manager43 ~]# cat /etc/hosts
127.0.0.1   localhost localhost.localdomain localhost4 localhost4.localdomain4
::1         localhost localhost.localdomain localhost6 localhost6.localdomain6
# manager的hosts复制到node
[root@manager ~]# scp /etc/hosts {user of node1}@{ip of node1}:/etc/hosts
[root@manager ~]# scp /etc/hosts {user of node2}@{ip of node2}:/etc/hosts
# 开放服务器端口（实现节点间互通）
firewall-cmd --zone=public --add-port 7946/tcp --permanent
firewall-cmd --zone=public --add-port 7946/udp --permanent
firewall-cmd --zone=public --add-port 4789/udp --permanent
firewall-cmd --zone=public --add-port 4789/tcp --permanent
systemctl reload firewalld
# 防火墙关闭或开放端口。
[root@manager ~]# systemctl disable firewalld.service
[root@manager ~]# systemctl stop firewalld.service
````

### 3.2 Swarm创建

````bash
# 创建Swarm集群
[root@manager ~]# docker swarm init --advertise-addr {ip of manager}
...记录以下信息
docker swarm join --token SWMTKN-1-5d96eebzhqmshvzg4lps08fgtfgvhq9891fssqtl8itykevaxd-943mjtl1ez4ogs7dntitc8lwz 192.168.177.138:2377
...
# Swarm信息
[root@manager ~]# docker info
...
Swarm: active
  NodeID: i3j76y43hk1damhmiy111vhws
  Is Manager: true
  ClusterID: o8nrnqql62r62kn9lndtjh7oz
  Managers: 1
  Nodes: 2
  Default Address Pool: 10.0.0.0/8  
  SubnetSize: 24
  Data Path Port: 4789
  Orchestration:
   Task History Retention Limit: 5
  Raft:
   Snapshot Interval: 10000
   Number of Old Snapshots to Retain: 0
   Heartbeat Tick: 1
   Election Tick: 10
  Dispatcher:
   Heartbeat Period: 5 seconds
  CA Configuration:
   Expiry Duration: 3 months
   Force Rotate: 0
  Autolock Managers: false
  Root Rotation In Progress: false
  Node Address: 192.168.177.138
  Manager Addresses:
   192.168.177.138:2377
...
# 加入节点
[root@node1 ~]# docker swarm join --token SWMTKN-1-5d96eebzhqmshvzg4lps08fgtfgvhq9891fssqtl8itykevaxd-943mjtl1ez4ogs7dntitc8lwz 192.168.177.138:2377
# 管理节点
[root@manager ~]# docker node update --availability active node1
````





