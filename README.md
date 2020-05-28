# Kafka
Kafka is a distributed streaming platform. It runs in a cluster of one or more servers.
Used to publish/subscribe, store, and process streams of records (key:value + timestamp)
Kafka stores streams of records in categories called topics.

It stores each topic in multiple partitions (for scalability), many consumers can **subscribe** to a topic and read about it. Similarly many producers can produce content(articles regarding a topic) and **publish** it to that topic's stream of records. 
Stores partitioned log containing offset. Refer [Diagram](https://kafka.apache.org/25/images/log_anatomy.png)

Each record has an offset id, a consumer usually goes sequentially, but if need be can override the offset and get old data. metadata contains offset id where a consumer last left reading.

Each individual partition must fit on the servers that host it, but a topic may have many partitions. Each partition spans multiple servers and is replicated using master/slave.
Ex. Servers s1, s2, s3, s4 form a kafka cluster. partition p1 is hosted on s1,s2 (p1 completely fits in s1 as well as s2) and partition p2 is hosted on s3, s4. Topic t1 has p1 and p2 as its partitions. s1 is a leader(writes to p1), and s2 is a follower(replicates p1 from s1). Refer [drawing](https://kafka.apache.org/25/images/consumer-groups.png)

Kafka guarantees that producer records will go in sequentially and consumers will see them in the order they are published. 

Enterprise Messaging Systems:
Queuing: enque records and then deque to one of your consumer, this allows to divide processing
publish-subscribe: publish records sequentially and broadcast to all consumers, this cannot scale/imporve processing in any way.
Kafka: generalizes this by using consumer groups. Each consumer group can have multiple consumers, the record is broadcast to the group and then it can be divided among consumers to scale processing.

Kafka allows producers to wait for acknowledgement of their writes. A write is only completed when it is written and replicated to all partitions. It works like a distributed file system in this case.

Streams processor: input is streams of records, you can do non-trivial processing on published records before sending them out using the streams API

To sum up: Kafka can process historical, stored data, it can also process live data as it comes. It replicates data thus addressing fault-tolerance (providing reliability). Using only offset id's it provides a low-latency service. 


question: 
Does a partition need to fit entirely on a server?
Is it similar to hadoop?


# References
Basics: https://kafka.apache.org/intro.html

