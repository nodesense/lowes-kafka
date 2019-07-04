
Open New Terminal

$KAFKA_HOME/bin/kafka-server-start $KAFKA_HOME/etc/kafka/server-1.properties


Open New Terminal

$KAFKA_HOME/bin/kafka-server-start $KAFKA_HOME/etc/kafka/server-2.properties


Open New Terminal

$KAFKA_HOME/bin/kafka-server-start $KAFKA_HOME/etc/kafka/server-3.properties


open new terminal

kafka-topics --create --zookeeper localhost:2181 --replication-factor 3 --partitions 3 --topic messages

kafka-topics --describe --zookeeper localhost:2181 --topic messages

kafka-console-producer --broker-list localhost:9092 --topic messages --property "parse.key=true" --property "key.separator=:"

kafka-console-consumer --bootstrap-server localhost:9092 --topic messages --from-beginning --property print.key=true --property print.timestamp=true