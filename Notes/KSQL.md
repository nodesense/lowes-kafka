
```
> ksql 


SHOW STREAMS;

SHOW TABLES;

SHOW TOPICS;

SHOW QUERIES;


ksql-datagen quickstart=users format=avro topic=users maxInterval=5000
ksql-datagen quickstart=pageviews format=avro topic=pageviews maxInterval=5000


{"ROWTIME":1552105167062,
 "ROWKEY":"User_5",
  "registertime":1494126392062,
  "userid":"User_5",
  "regionid":"Region_9",
  "gender":"OTHER"}

CREATE STREAM users_stream (userid varchar, regionid varchar, gender varchar) WITH \
(kafka_topic='users', value_format='AVRO');


DESCRIBE users_stream;

Non Persistent

select userid, regionid, gender from users_stream where gender='FEMALE';

Ctrl + c to exit

Persistent query, create a kafka topic called users_female
with attributes, userid, regionid, persist the records into Kafka Topics

CREATE STREAM users_female AS \
SELECT userid AS userid, regionid \
FROM users_stream \
where gender='FEMALE';


 1552106259683 | 'User_4' | 'Page_80' ]) ts:1552106260558

topic: pageviews



CREATE STREAM pageviews_stream (userid varchar, pageid varchar) WITH \
(kafka_topic='pageviews', value_format='AVRO');

select * from pageviews_stream;


users_stream
pageviews_stream

Joined output

pageviews_enriched_stream


CREATE STREAM pageviews_enriched_stream AS \
SELECT users_stream.userid AS userid, pageid, regionid, gender \
FROM pageviews_stream \
LEFT JOIN users_stream \
  WITHIN 1 HOURS \
  ON pageviews_stream.userid = users_stream.userid;

CREATE STREAM pageviews_enriched_stream_males AS \
SELECT users_stream.userid AS userid, pageid, regionid, gender \
FROM pageviews_stream \
LEFT JOIN users_stream \
  WITHIN 1 HOURS \
  ON pageviews_stream.userid = users_stream.userid \
  WHERE gender = 'MALE';


select *  from pageviews_enriched_stream;

select *  from pageviews_enriched_stream_males;

CREATE TABLE pageviews_region_table \
        WITH (VALUE_FORMAT='avro') AS \
        SELECT gender, regionid, COUNT(*) AS numusers \
        FROM pageviews_enriched_stream \
        WINDOW TUMBLING (size 30 second) \
        GROUP BY gender, regionid \
        HAVING COUNT(*) >= 1;

select *  from pageviews_region_table;

PERSISTED QUERY FOR TABLE


CREATE TABLE pageviews_region_gt_10_table AS \
SELECT gender, regionid, numusers \
FROM pageviews_region_table \
where numusers > 10;

select *  from pageviews_region_gt_10_table;




KSQL
    STREAM - Produce into Another Kafka Topic, subscribe from source topic
        KSTREAM
    TABLE - Produce into Another Kafka Topic, subscribe from source topic
        KTABLE
    QUERY [TABLE, STREAM]
        Persisted
            Store results into Another Kafka Topic, subscribe from source topic

            SHOW QUERIES;
            EXPLAIN <QUERY_ID>;
            TERMINATE <QUERY_ID>;
        Non-persisted

---


Control Center DEMO


ksql-datagen quickstart=pageviews format=avro topic=pageviews maxInterval=50


```