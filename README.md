# project
spring-boot+kafka

## Kafka安装
### Docker镜像
- zookeeper
- wurstmeister/kafka
- sheepkiller/kafka-manager

### 容器启动
- zookeeper
```
docker run --name some-zookeeper \
--restart always \
-p 2181:2181 \
-d zookeeper
```

- wurstmeister/kafka
```
docker run --name kafka \
-p 9092:9092 \
-e KAFKA_ADVERTISED_HOST_NAME=192.168.3.36 \
-e KAFKA_CREATE_TOPICS="test:1:1" \
-e KAFKA_ZOOKEEPER_CONNECT=192.168.3.36:2181 \
-d  wurstmeister/kafka
```

- sheepkiller/kafka-manager
```
docker run -itd \
--restart=always \
--name=kafka-manager \
-p 9000:9000 \
-e ZK_HOSTS="192.168.3.36:2181" \
sheepkiller/kafka-manager
```

### kafka配置
- 添加Topic
```
docker exec -it kafka /bin/bash

/opt/kafka/bin/kafka-topics.sh --create --zookeeper 192.168.3.36:2181 --replication-factor 1 --partitions 1 --topic monitor
```

### 基本操作
- 发送消息
```
/opt/kafka/bin/kafka-console-producer.sh --broker-list  192.168.3.36:9092 --topic monitor
```

- 接收消息
```
/opt/kafka/bin/kafka-console-consumer.sh --bootstrap-server 192.168.3.36:9092 --topic monitor --from-beginning
```

