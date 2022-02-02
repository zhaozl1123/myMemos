---
layout: post
title:  "基于Docker的MQTT部署"
date:   2022-01-15 15:23:00 +0800
categories: [mqtt, docker-install]
tags: [mqtt, mqtt-deploy, mqtt-docker]
author:
  name: zhoazl1123
  link: https://github.com/zhaozl1123
---

### 1. 部署
```bash
docker pull emqx/emqx:v4.0.0
docker run -it --name emqx -p 1883:1883 -p 8083:8083 -p 8883:8883 -p 8084:8084 -p 18083:18083 emqx/emqx:v4.0.0
user:admin psw:public1
```


|       协议         |        端口        |     说明      |
|       -----       |       -----       |   -----       |
|       mqtt:ssl    |       8883        ||
|mqtt:tcp           |0.0.0.0:1883       |TCP协议端口，可以用于数据生产|
|mqtt:tcp           |127.0.0.1:11883    ||
|http:dashboard     |18083              |   EMQ Web前端  |
|http:management    |8081               ||
|mqtt:ws            |8083               |Websocket协议端口，可用于ws协议的数据消费|
|mqtt:wss           |8084               ||

