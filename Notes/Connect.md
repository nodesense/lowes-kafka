Connect

Source, read from file/database/etc and publish to KAfka Topic
    Data stored into the file,
        on the file change, pull the line, and publish to kafka topic
        
    Database,
        insert/update a record, push to kafka
        
Sink, read from kafka topic, write to file/HDFS/database etc

Task 1: Read from file change, push to kafka topics

mkdir krish
cd krish 

```
nano krish-file-source.properties
```

paste below connect

```
name=krish-file-source
connector.class=FileStreamSource
tasks.max=1
file=/root/krish/input-file.txt
topic=krish-file-content
```

Ctrl + 

open second shell on server [ssh again]

```
kafka-console-consumer --bootstrap-server localhost:9092 --topic krish-file-content --from-beginning
```


### To know existing running connectors

```
confluent status connectors

```

### to start the connector


confluent load krish-file-source -d /Users/krish/krish/krish-file-source.properties

### Know the status of the connector

confluent status krish-file-source


### To stop the connector

confluent unload krish-file-source


### Echo command to feed the data

ensure you are in the same directory 

```
echo "line 1" >> input-file.txt
```
---------

## Sink from Kafka Topic to File



```
nano krish-file-sink.properties
```

paste below connect


```
name=krish-file-sink
connector.class=FileStreamSink
tasks.max=1
file=/root/krish/output-file.txt
topics=krish-file-content
```


### Create a output file

```
touch output-file.txt
```

### to start the connector


```
confluent load krish-file-sink -d /Users/krish/krish/krish-file-sink.properties
```

### Know the status of the connector
```
confluent status krish-file-sink
```
### To stop the connector
```
confluent unload krish-file-sink

```

Write to topic, then it goes to file

```
kafka-console-producer --broker-list localhost:9092 --topic krish-file-content --property key.serializer=org.apache.kafka.common.serialization.StringSerializer --property value.serializer=org.apache.kafka.common.serialization.StringSerializer
```
