
Environment Variable, Windows

Press start menu, search Environ.. [Select Environment For your account]

Add new Environment
KAFKA_HOME

The value should be c:\confluent-5.2.2

Edit/Add PATH
c:\confluent-5.2.2\bin\windows

Click Save

--
MAC

cd ~

vi .bash_profile

~/.bash_profile

export KAFKA_HOME=/Users/yourname/confluent-5.2.2
export PATH=$PATH:$KAFKA_HOME/bin

save and close the terminal

--WINDOWS

open command prompt

%KAFKA_HOME%\bin\windows\zookeeper-server-start.bat %KAFKA_HOME%\etc\kafka\zookeeper.properties

-- MAC
open terminal

$KAFKA_HOME/bin/zookeeper-server-start $KAFKA_HOME/etc/kafka/zookeeper.properties

Java 8 JDK
IDE: IntelliJ Community/Eclipse
Putty/GitBash

---