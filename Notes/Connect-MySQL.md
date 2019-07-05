# Task: Take the changes in mysql and publish to kafka topics


mysql -uroot

CREATE USER 'team'@'%' IDENTIFIED BY 'team1234';

GRANT ALL PRIVILEGES ON *.* TO 'team'@'%' WITH GRANT OPTION;

quit;

---

### setup the tables

```
mysql -uroot

CREATE DATABASE krish;

USE krish;

create table products (id int, name varchar(255), price int, create_ts timestamp DEFAULT CURRENT_TIMESTAMP , update_ts timestamp DEFAULT CURRENT_TIMESTAMP ON UPDATE CURRENT_TIMESTAMP );

 ```
 
 #### Setup the source connnector
 
```
touch krish-mysql-product-source.json
```
 
``` 
 
{
  "name": "krish-mysql-product-source",
  "config": {
    "connector.class": "io.confluent.connect.jdbc.JdbcSourceConnector",
    "key.converter": "io.confluent.connect.avro.AvroConverter",
    "key.converter.schema.registry.url": "http://k8.nodesense.ai:8081",
    "value.converter": "io.confluent.connect.avro.AvroConverter",
    "value.converter.schema.registry.url": "http://k8.nodesense.ai:8081",
    "connection.url": "jdbc:mysql://localhost:3306/krish?user=team&password=team1234",
    "_comment": "Which table(s) to include",
    "table.whitelist": "products",
    "mode": "timestamp",
     "timestamp.column.name": "update_ts",
    "validate.non.null": "false",
    "_comment": "The Kafka topic will be made up of this prefix, plus the table name  ",
    "topic.prefix": "krish-db-"
  }
}

```

To load connectors

```
confluent status connectors

```

```
confluent load krish-mysql-product-source -d krish-mysql-product-source.json
```

```
confluent status krish-mysql-product-source 
```


# To check if the data changes are published are not

```
kafka-avro-console-consumer --bootstrap-server localhost:9092 --topic krish-db-products --from-beginning
```


# to refer to schema registry on other machine

kafka-avro-console-consumer --bootstrap-server localhost:9092 --topic krish-db-products --from-beginning     --property schema.registry.url="http://k8.nodesense.ai:8081"




# Add data into db

```
mysql -uroot

USE krish;


insert into products(id, name, price) values(1, "P1", 100);

insert into products(id, name, price) values(2, "P2", 200);

select * from products;

update products set price=300 where id=1;

```