# Kafka


## 生产者模型

````python
from kafka import KafkaProducer as producer

_producer = producer(bootstrap_servers=["127.0.0.1:9092"],
                             key_serializer=lambda x: json.dumps(x).encode("utf-8"),
                             value_serializer=lambda x: json.dumps(x).encode("utf-8"))
for tag in range(tagStart, tagEnd):
    _producerInfo = _producer.send("training_info", _info, partition=0)
	result = _producerInfo.get(timeout=2)
````

## 消费者模型

````python
from kafka import KafkaConsumer

consumer = KafkaConsumer('training_info', bootstrap_servers=['127.0.0.1:9092'])
for msg in consumer:
    recv = "%s:%d:%d: key=%s value=%s" % (msg.topic, msg.partition, msg.offset, msg.key, msg.value)
    print(recv)
# training_info:0:239: key=b'null' value=b'{"Tag": 0.14, "StartTime": "2020-12-04 09:46:42", "EndTime": "2020-12-04 09:46:42", "LastTime": 0.46}'
# training_info:0:240: key=b'null' value=b'{"Tag": 0.14, "StartTime": "2020-12-04 09:46:42", "EndTime": "2020-12-04 09:46:43", "LastTime": 0.49}'
# training_info:0:241: key=b'null' value=b'{"Tag": 0.15, "StartTime": "2020-12-04 09:46:43", "EndTime": "2020-12-04 09:46:43", "LastTime": 0.46}'
# training_info:0:242: key=b'null' value=b'{"Tag": 0.15, "StartTime": "2020-12-04 09:46:43", "EndTime": "2020-12-04 09:46:44", "LastTime": 0.59}'
# training_info:0:243: key=b'null' value=b'{"Tag": 0.16, "StartTime": "2020-12-04 09:46:44", "EndTime": "2020-12-04 09:46:45", "LastTime": 0.61}'
# training_info:0:244: key=b'null' value=b'{"Tag": 0.17, "StartTime": "2020-12-04 09:46:45", "EndTime": "2020-12-04 09:46:45", "LastTime": 0.47}'
# training_info:0:245: key=b'null' value=b'{"Tag": 0.17, "StartTime": "2020-12-04 09:46:45", "EndTime": "2020-12-04 09:46:45", "LastTime": 0.49}'
# training_info:0:246: key=b'null' value=b'{"Tag": 0.17, "StartTime": "2020-12-04 09:46:45", "EndTime": "2020-12-04 09:46:46", "LastTime": 0.59}'
````

## Docker部署

```bash
docker run -it -p 50001:50001 --network=bridge --name=mysql_inspect  mysql_inspect:latest  # 部署mysql_inspect， 172.17.0.2
docker run -it --name zookeeper --network=bridge  -p 2181:2181 zookeeper:latest  # 部署zookeeper, 172.17.0.3
docker run -it --name kafka -p 9092:9092 -p 9999:9999 -e KAFKA_BROKER_ID=1 -e KAFKA_ZOOKEEPER_CONNECT=172.17.0.3:2181 -e KAFKA_ADVERTISED_HOST_NAME=172.17.0.4 -e KAFKA_ADVERTISED_LISTENERS=PLAINTEXT://172.17.0.4:9092 -e KAFKA_LISTENERS=PLAINTEXT://0.0.0.0:9092 -e JMX_PORT=9999 -e KAFKA_JMX_OPTS="-Dcom.sun.management.jmxremote -Dcom.sun.management.jmxremote.authenticate=false -Dcom.sun.management.jmxremote.ssl=false -Djava.rmi.server.hostname=172.17.0.3 -Dcom.sun.management.jmxremote.rmi.port=9999" wurstmeister/kafka:latest  # 部署kafka, 172.17.0.4
```

