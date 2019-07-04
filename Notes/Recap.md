
Broker  
    - Storing Messages
        bytes
    - Message {key: bytes, value: bytes}
    - Log Retention 
            -- Applied to topics
                    Topic 1 -  1 day
                    Topci 2 - 7 days
                    .. --- 30 days

    log.dirs=/tmp/kafka-logs
            broker data files, NO TOPIC Information

                topic-name-partition-id
                messsges-0
                    0000000000000.log - all key/value messsages [ 1 GB default size,]
                            log.segment.bytes=1073741824

                    0000000000000.index - offset number to message file location
                    0000000000000.timeindex - inserting time to offset number

                messages-1

Consumer
        Subscribe [topics, internally it is for partition]
        Poll - pull 

        Consumer Group - Unique ID for the similar purpose consumer application
                props.put(GROUP_ID_CONFIG, "messages-consumer-email"); // offset, etc, TODO

        emails-group
                    consumer1 [partition 0, 1] - send email
                    consumer2 [partition 2, 3] - send email
                    consumer3 [partition 4,5] - send email

        sms-group
                    consumer1 [partition 0] - send sms
                    consumer2 [partition 2] - send sms
                    consumer3 [partition 3] - send sms
                    consumer4 [partition 4] - send sms
                    consumer5 [partition 5] - send sms
                    consumer6 [partition 1] - send sms
                    consumer7 [no partition] - send sms, idle
            
        Consumer [Group] Offset
                    -- maintain the last commited offset by the consumer application
                    -- when the consumer restart, it can get message from last commited offset

                        props.put(ENABLE_AUTO_COMMIT_CONFIG, "auto");
                        props.put(AUTO_COMMIT_INTERVAL_MS_CONFIG, "1000");


                        props.put(ENABLE_AUTO_COMMIT_CONFIG, "false");
                        consumer.commitSync(); // manual commit, set the offset

                        
        commit - auto/manual commit
                auto - handled by Kafka SDK, as soon message pulled by consumer, commit offset send to broker
                manual - pull the data, process the data, finally commit the offset 
Producer
        Partition decided by producer
        Key Serializer - convert data to bytes
        Value Serializer - convert data to bytes

        Ack 
                0  - Message is received by the broker from network. not commited to disk.
                1 - Lead broker for partition, have the data in Harddisk
                all  - replicas = Lead + all replicas should have the data committed to Harddisk

ZooKeeper [2181]
    -- Meta, Topics, Partitions, who is lead for the partition
    -- maintain heartbeat with brokers
    -- elect leader for partitions
    -- database, flat file
    -- in-memory, write the snapshot to files
    -- hierachy structure [tree]
    -- must be run the cluster

Consumer Group

Topics
Partitions
Offets
Replicas
