# Task: Take the changes in mysql and publish to kafka topics


mysql -uroot

CREATE USER 'team'@'%' IDENTIFIED BY 'team1234';

GRANT ALL PRIVILEGES ON *.* TO 'team'@'%' WITH GRANT OPTION;
