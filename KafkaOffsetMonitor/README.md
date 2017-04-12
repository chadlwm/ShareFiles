# KafkaOffsetMonitor

kafka 0.9.x save the consumers offset with kafka as default, not zookeeper.
so  [KafkaOffsetMonitor-assembly-0.2.1.jar](https://github.com/quantifind/KafkaOffsetMonitor) couldnot see anything about consumers, at the same time,  KafkaOffsetMonitor-assembly-0.2.1.jar not support option `--offsetStorage` as the [doc](https://github.com/quantifind/KafkaOffsetMonitor) description.

But, we can rebuild from source, new KafkaOffsetMonitor's version will be 0.3.0, this version supperts option `--offsetStorage`.

all the steps as follow:

```
# java
java -version
Picked up _JAVA_OPTIONS: -Djava.net.preferIPv4Stack=true
java version "1.8.0_121"
Java(TM) SE Runtime Environment (build 1.8.0_121-b13)
Java HotSpot(TM) 64-Bit Server VM (build 25.121-b13, mixed mode)

# install sbt
echo "deb https://dl.bintray.com/sbt/debian /" | sudo tee -a /etc/apt/sources.list.d/sbt.list
sudo apt-key adv --keyserver hkp://keyserver.ubuntu.com:80 --recv 2EE0EA64E40A89B84B2DF73499E82A75642AC823
sudo apt-get update
sudo apt-get install sbt

git clone --depth=50 --branch=master git://github.com/quantifind/KafkaOffsetMonitor.git 

# run test
sbt ++2.10.3 test

# rebuild
sbt ++2.10.3 assembly
```

then you will get `KafkaOffsetMonitor-assembly-0.3.0-SNAPSHOT.jar`

if you donnot want to build it by yourself, you can download my build one: [here](KafkaOffsetMonitor-assembly-0.3.0-SNAPSHOT.jar)

enjoy your time 

```
java -cp KafkaOffsetMonitor-assembly-0.3.0-SNAPSHOT.jar \
     com.quantifind.kafka.offsetapp.OffsetGetterWeb \
     --offsetStorage kafka \
     --zk 127.0.0.1:2181 \
     --port 18080 \
     --refresh 10.seconds \
     --retain 2.days
```


more details to see [here](https://github.com/quantifind/KafkaOffsetMonitor)
