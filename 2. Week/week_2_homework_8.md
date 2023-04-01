### 15.

```
from kafka.admin import KafkaAdminClient, NewTopic

admin_client = KafkaAdminClient(bootstrap_servers=['localhost:9092', 'localhost:9292'],
                                client_id='dataops_client')

print(admin_client.list_topics())
#  ['test1', 'test', 'test2', '__consumer_offsets']

def create_a_new_topic(admin_client, topic_name="example-topic", num_partitions=1, replication_factor=1):

    if topic_name not in admin_client.list_topics():
        create_topic1 = NewTopic(name=topic_name, num_partitions=num_partitions, replication_factor=replication_factor)
        try:
            admin_client.create_topics(new_topics=[create_topic1], validate_only=False)
        except:
            print('kafka.errors.TopicAlreadyExistsError')


create_a_new_topic(admin_client, topic_name="homework_topic_1", num_partitions=1, replication_factor=1)

print(admin_client.list_topics())

admin_client.close()
```
