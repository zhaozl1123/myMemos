# Kafka安装

## 安装
```bash
wget https://mirrors.tuna.tsinghua.edu.cn/apache/kafka/2.6.0/kafka_2.12-2.6.0.tgz
tar xf ./kafka_2.12-2.6.0.tgz -C /usr/local/
cd /usr/local
ln -s /usr/local/kafka_2.12-2.6.0 /usr/bin/kafka
```

````bash
[root@localhost bin]# /usr/local/kafka/bin/kafka-server-start.sh ../config/server1.properties
[root@localhost bin]# /usr/local/kafka/bin/zookeeper-server-start.sh ../config/zookeeper.properties
````

## 配置
### server1.properties
````bash
# /usr/local/kafka_2.12-2.6.0/config
broker.id=0
listeners=PLAINTEXT://127.0.0.1:9092
log.dirs=kafka-logs
zookeeper.connect=localhost:2181
offsets.topic.replication.factor=1
````

### zookeeper.properties
````bash
# /usr/local/kafka_2.12-2.6.0/config
dataDir=/tmp/zookeeper
clientPort=2181
maxClientCnxns=0
admin.enableServer=false
````
