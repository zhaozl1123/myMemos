---
layout: post
title:  "MQTT的使用"
date:   2022-01-15 15:25:00 +0800
categories: [mqtt, usage]
tags: [mqtt, mqtt-usage]
author:
  name: zhoazl1123
  link: https://github.com/zhaozl1123
---

### 1.数据的生产
```Python
import json
import paho.mqtt.client as mqtt
import time

client_id = 'client02'
HOST = "192.168.177.145"
PORT = 1883  # TCP协议的端口

data = {
    "type": 2,
    "timestamp": time.time(),
    "messageId": "9fcda359-89f5-4933-xxxx",
    "command": "xx/recommend",
    "data": {
        "openId": "xxxx",
        "appId": "xxxx",
        "recommendType": "temRecommend"
    }
}

client = mqtt.Client(client_id)
client.connect(HOST, PORT, 60)
for i in range(1000):
    data['type'] = i
    obj = client.publish("data", payload=json.dumps(data), qos=0)
    time.sleep(1.5)
    print(">>>", i, obj.is_published())
```

### 2.数据的消费
```python
import paho.mqtt.client as mqtt


TASK_TOPIC = 'data'  # 客户端发布消息主题

client_id = 'client02'
client = mqtt.Client(client_id, transport='tcp')
client.connect("192.168.177.145", 1883, 60)  # 链接


def on_connect(client, userdata, flags, rc):
    client.subscribe("data")         # 订阅消息


def on_message(client, userdata, msg):
    print("主题:"+msg.topic+" 消息:"+str(msg.payload.decode('utf-8')))


def on_subscribe(client, userdata, mid, granted_qos):
    print("On Subscribed: qos = %d" % granted_qos)


if __name__ == '__main__':
    client.on_connect = on_connect
    client.on_message = on_message
    client.on_subscribe = on_subscribe
    client.loop_forever()
```

### 3.可能的用户名与密码

```
id:admin
pwd:public
```