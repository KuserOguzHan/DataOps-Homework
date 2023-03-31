### 1. Start Kafka local

1. Start zookeeper
```
[train@trainvm]$ sudo systemctl start zookeeper
```

2. Start kafka server
```
[train@trainvm]$ sudo systemctl start kafka
```

3. Status kafka server
```
[train@trainvm]$ sudo systemctl status kafka
```

### 2. List topics
` [train@trainvm]$ kafka-topics.sh --bootstrap-server localhost:9092 --list `

### 3. Create a topic

```
kafka-topics.sh --bootstrap-server localhost:9092 \
--create --topic atscale \
--replication-factor 1 \
--partitions 2
```

```
kafka-topics.sh --bootstrap-server localhost:9092 --list
```


### 4. Describe a topic
```
kafka-topics.sh --bootstrap-server localhost:9092 \
--describe --topic atscale


Topic: atscale   PartitionCount: 2       ReplicationFactor: 1    Configs: segment.bytes=1073741824
        Topic: atscale   Partition: 0    Leader: 0       Replicas: 0     Isr: 0
        Topic: atscale   Partition: 1    Leader: 0       Replicas: 0     Isr: 0
      
```

### 5. Delete a topic
```
kafka-topics.sh --bootstrap-server localhost:9092 \
--delete --topic atscale
```

```
kafka-topics.sh --bootstrap-server localhost:9092 --list
```
