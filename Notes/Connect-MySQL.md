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