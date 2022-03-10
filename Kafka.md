# Kafka
- why message queue
    - syncronized model
        - 1000 people while sever can only handle 100 requests
        - not efficient, affect user experience
    - asyncronized model
        - people -> s1 -> MQ -> s2
    - loosely coupled
    - cache
    - flexible
    - asynchronized communication

- Message queue model
    - point to point (one to one)
    - publish and subscribe model (one to many)

### Kafka architecture

* Producer
    * why we need partition
    * ProderRecord(topic, partition, key)
    * the partition principle
    * partition 
    * key -> hashcode -> % 
    * round robin
    
* consumer
* consumer group
* broker
* topic
* partition
* replica
* leader
* follower

- TBD
    - 

    
 
