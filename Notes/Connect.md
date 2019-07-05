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

nano krish-file-source.properties

paste below connect

name=krish-file-source
connector.class=FileStreamSource
tasks.max=1
file=/root/krish/input-file.txt
topic=krish-file-content


Ctrl + 

open second shell on server [ssh again]

kafka-console-consumer --bootstrap-server localhost:9092 --topic krish-file-content --from-beginning



name=krish-file-sink
connector.class=FileStreamSink
tasks.max=1
file=/root/krish/output-file.txt
topics=krish-file-content


