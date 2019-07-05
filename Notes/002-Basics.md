Only for Servers 

wget https://raw.githubusercontent.com/nodesense/kafka-workshop/master/system-setup.sh -O - -o /dev/null|bash

> reboot

> confluent start



Topics, PArition Info, replications, Brokers info - meta data are stored into Zookeeper

The data/messages are stored into Kafka Broker




kafka-topics --create --zookeeper localhost:2181 --replication-factor 1 --partitions 1 --topic test

kafka-topics --list --zookeeper localhost:2181

-- Kafka Console producer

Open forth command prompt window

kafka-console-producer --broker-list localhost:9092 --topic test

Open fifth command prompt window

kafka-console-consumer --bootstrap-server localhost:9092 --topic test

kafka-console-consumer --bootstrap-server localhost:9092 --topic test --from-beginning


kafka-topics --describe --zookeeper localhost:2181 --topic test


kafka-topics --create --zookeeper localhost:2181 --replication-factor 1 --partitions 3 --topic greetings

kafka-topics --describe --zookeeper localhost:2181 --topic greetings

kafka-console-producer --broker-list localhost:9092 --topic greetings --property "parse.key=true" --property "key.separator=:"

kafka-console-consumer --bootstrap-server localhost:9092 --topic greetings --from-beginning --property print.key=true --property print.timestamp=true

kafka-topics --create --zookeeper localhost:2181 --replication-factor 1 --partitions 3 --topic greetings

kafka-topics --create --zookeeper localhost:2181 --replication-factor 1 --partitions 3 --topic greetings2


 