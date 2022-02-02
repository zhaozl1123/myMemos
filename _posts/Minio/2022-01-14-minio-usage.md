---
layout: post
title:  "Minio的使用"
date:   2022-01-14 16:30:00 +0800
categories: [minio, usage]
tags: [minio-usage, minio-docker]
author:
  name: zhaozl1123
  link: https://github.com/zhozl1123
---

## Install

Server上的部署
```bash
docker run -p 9000:9000 -e "MINIO_ROOT_USER=admin" -e "MINIO_ROOT_PASSWORD=minioadmin" minio/minio server /data
```

:::warning 注意
- 注意修改firewall，开放9000端口。
- 如果使用Vmware，需要使用NAT挂载端口至宿主机
:::

## 使用

Client上的使用
```python
from minio import Minio
from minio.error import S3Error

# 初始化
client = Minio("localhost:19000", access_key="minioadmin", secret_key="minioadmin", secure=False)  # 需要人为指定http，否则报Retries Times错误

# Bucket存在状态检查
bucketExistsCheck = client.bucket_exists("my-bucket")

# 创建Bucket
client.make_bucket("my-bucket")

# 上传对象
client.fput_object("my-bucket", "targetName", "sourcePath")  # targetName:Bucket中的对象名称，sourcePath:对象地址

# 读取对象
client.get_object("my-bucket", "targetName")
```
