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

### 5. Create New Topic For Question 4

[train@trainvm]$ 
```
kafka-topics.sh --bootstrap-server localhost:9092 \
--create --topic churn \
--partitions 3 \
--replication-factor 1
```

[train@trainvm]$ 
```
kafka-topics.sh --bootstrap-server localhost:9092 --list
```

### 6. Producing with data-generator
- Use instructions in this repo to use data generator

```
[train@trainvm]$ git clone https://github.com/erkansirin78/data-generator.git
```

```
[train@trainvm]$ cd data-generator/
```

```
[train@trainvm data-generator]$ python3 -m virtualenv datagen
```

```
[train@trainvm data-generator]$ source datagen/bin/activate
```
 
```
(datagen) [train@trainvm data-generator]$ pip install -r requirements.txt
```

### 7. Create Consumer 

- You open 3 terminal
- Terminal 2,3,4
  
```  
[train@trainvm]$ kafka-console-consumer.sh --bootstrap-server localhost:9092 --topic churn --group churn_group
```

### 8. Produce dataset 

- Terminal 1
```
(datagen) [train@trainvm data-generator]$  python dataframe_to_kafka.py -i ~/datasets/Churn_Modelling.csv -t churn -k 1
```


### 9. Delete a topic
```
(datagen) [train@trainvm data-generator]$ kafka-topics.sh --bootstrap-server localhost:9092 --delete --topic churn
```
```
(datagen) [train@trainvm data-generator]$ kafka-topics.sh --bootstrap-server localhost:9092 --delete --topic atscale
```

```
kafka-topics.sh --bootstrap-server localhost:9092 --list
```


### 10. Docker-Compose Up

- If docker-compose is not run, you should track following steps.
- You should delete kafka1, kafka2, kafka3 and build docker-compose again.
- Chechk week.2.1.md 

```
[train@trainvm zookeeperless_kafka]$ docker-compose ps
```

```
[train@trainvm ~]$ cd dataops7/kafka/zookeeperless_kafka/
```

```
[train@trainvm zookeeperless_kafka]$ sudo systemctl start docker
```

```
[train@trainvm zookeeperless_kafka]$ sudo systemctl status docker
```

```
[train@trainvm zookeeperless_kafka]$ docker-compose up -d
```


### 11. Creata Topic with Admin_client.py in Pycharm

- Open pycharm editor and create new project and admin.client

```
from kafka.admin import KafkaAdminClient, NewTopic, ConfigResource, ConfigResourceType
import time

admin_client = KafkaAdminClient(bootstrap_servers=['localhost:9092', 'localhost:9292'],
                                client_id='dataops_client')

# List topics
print("Created topics", admin_client.list_topics())

# Create a topic
try:
    homework1 = NewTopic(name='homework1', num_partitions=2, replication_factor=2)

    admin_client.create_topics(new_topics=[homework1])
except:
    print("Topics are already exist.")


# List topics
time.sleep(2)
print("After create topics", admin_client.list_topics())
```

```
[train@trainvm]$ kafka-topics.sh --bootstrap-server localhost:9092 --list
```

### 12.

```
from kafka import KafkaProducer
import time


my_producer = KafkaProducer(bootstrap_servers=['localhost:9092', 'localhost:9292', 'localhost:9392'],
                           client_id='my_producer')

regions = ['Ic Anadolu','Doğu Anadolu','Karadeniz', 'Akdeniz','Marmara','Ege','Güneydogu Anadolu']


for i, val in enumerate(regions):
    my_producer.send(topic='homework1',
                 key=f'{i+1}'.encode("utf-8"),
                 value=f'{val}'.encode("utf-8"))


my_producer.close()
```















