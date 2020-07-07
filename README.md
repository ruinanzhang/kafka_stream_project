# kafka_stream_project
Module 1 for data connector: 
Read data from various clients (SQL or NoSQL data) - > convert the data into JSON files -> Dump the JSON files on Kafka topic using the Kafka connector  
**1.Start Zookeeper:** 

`bin/zookeeper-server-start.sh config/zookeeper.properties`

**2. Start Kafka**  

`bin/kafka-server-start.sh config/server.properties` 

**3. Create Kafka topics** 

For input topic:

`bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 2 --topic demo-app-input`

For output topic:

`bin/kafka-topics.sh --create --zookeeper localhost:2181 --replication-factor 1 --partitions 2 --topic demo-app-output`

**Check if topics created successfully**

`bin/kafka-topics.sh --bootstrap-server localhost:9092 --describe`

**4.launch a Kafka consumer**

`bin/kafka-console-consumer.sh --bootstrap-server localhost:9092 \
    --topic demo-app-output \
    --from-beginning \
    --formatter kafka.tools.DefaultMessageFormatter \
    --property print.key=true \
    --property print.value=true \
    --property key.deserializer=org.apache.kafka.common.serialization.StringDeserializer \
    --property value.deserializer=org.apache.kafka.common.serialization.LongDeserializer`
    
**5.launch the streams application**
