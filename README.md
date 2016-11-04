[![Build Status](https://travis-ci.org/alibaba/dubbo.svg?branch=master)](https://travis-ci.org/alibaba/dubbo) [![Gitter](https://badges.gitter.im/alibaba/dubbo.svg)](https://gitter.im/alibaba/dubbo?utm_source=badge&utm_medium=badge&utm_campaign=pr-badge)

Dubbo is a distributed, high performance RPC framework which empowers applications with service import/export capabilities.

It contains three key parts, which include:

* **Remoting**: a network communication framework providing sync-over-async and request-response messaging.
* **Clustering**: a remote procedure call abstraction with load-balancing/failover/clustering capabilities.
* **Registration**: a service directory framework for service registration and service event publish/subscription

For more details, please refer to [wiki](https://github.com/alibaba/dubbo/wiki) or [dubbo.io](http://dubbo.io).

## Quick Start

## Source Building


0. Install the git and maven command line:
```sh
yum install git
or: apt-get install git
cd ~
wget http://www.apache.org/dist//maven/binaries/apache-maven-3.2.2-bin.tar.gz
tar zxvf apache-maven-3.2.2-bin.tar.gz
vi .bash_profile
append: export PATH=$PATH:~/apache-maven-3.2.2/bin
source .bash_profile
```


0. Checkout the dubbo source code:

```sh
cd ~
git clone https://github.com/EPAM-CN/dubbo.git
```

0. Import the dubbo source code to intellj/eclipse project:

```sh
    Then demo code struct in the project is below:
    * Start DEMO:
        * ${basedir}/dubbo-demo/dubbo-demo-provider/src/test/java/com/alibaba/dubbo/demo/provider/DemoProvider.java
        * ${basedir}/dubbo-demo/dubbo-demo-consumer/src/test/java/com/alibaba/dubbo/demo/consumer/DemoConsumer.java
        * ${basedir}/dubbo-simple/dubbo-monitor-simple/src/test/java/com/alibaba/dubbo/monitor/simple/SimpleMonitor.java
        * ${basedir}/dubbo-simple/dubbo-registry-simple/src/test/java/com/alibaba/dubbo/registry/simple/SimpleRegistry.java
    * Edit Config:
        * ${basedir}/dubbo-demo/dubbo-demo-provider/src/main/resources/META-INF/spring/dubbo-demo-provider.xml
        * This file is the config file for dubbo provider
        * ${basedir}/dubbo-demo/dubbo-demo-consumer/src/main/resources/META-INF/spring/dubbo-demo-consumer.xml
        * This file is the config file for dubbo consumer
        * ${basedir}/dubbo-simple/dubbo-monitor-simple/src/test/resources/dubbo.properties
        * This file is the config file for dubbo monitor
        * ${basedir}/dubbo-simple/dubbo-registry-simple/src/test/resources/dubbo.properties
        * This file is the config file for dubbo registry
```

0. Build the dubbo binary package:

```sh
cd ~/dubbo
mvn clean install -Dmaven.test.skip
```
## Demo Scenario1: multicast registry
0. change registry setting in config files:

```sh
* ${basedir}/dubbo-demo/dubbo-demo-provider/src/main/resources/META-INF/spring/dubbo-demo-provider.xml
* ${basedir}/dubbo-demo/dubbo-demo-consumer/src/main/resources/META-INF/spring/dubbo-demo-consumer.xml
edit config '<dubbo:registry address="multicast://224.5.6.7:1234"/>'
* ${basedir}/dubbo-simple/dubbo-monitor-simple/src/test/resources/dubbo.properties
edit config 'dubbo.registry.address=multicast://224.5.6.7:1234'
```
0. Run the demo provider with intellj/eclipse:

```sh
DemoProvider.java run main method
```

0. Run the demo consumer with intellj/eclipse:

```sh
 DemoConsumer.java run main method
 ```

0. Run the demo simple monitor with intellj/eclipse:

```sh
SimpleMonitor.java run main method
chrome open http://127.0.0.1:8080
```

## Demo Scenario2: dubbo registry
0. Start the simple registry with intellj/eclipse:

```sh
SimpleRegistry.java run main method
```

0. change registry setting in config files:

```sh
* ${basedir}/dubbo-demo/dubbo-demo-provider/src/main/resources/META-INF/spring/dubbo-demo-provider.xml
* ${basedir}/dubbo-demo/dubbo-demo-consumer/src/main/resources/META-INF/spring/dubbo-demo-consumer.xml
edit config '<dubbo:registry address="dubbo://127.0.0.1:9090"/>'
* ${basedir}/dubbo-simple/dubbo-monitor-simple/src/test/resources/dubbo.properties
edit config 'dubbo.registry.address=dubbo://127.0.0.1:9090'
```
0. restart  Demo:
```sh
 DemoProvider.java run main method
 DemoConsumer.java run main method
 SimpleMonitor.java run main method
 chrome open http://127.0.0.1:8080
```

## Demo Scenario3: zookeeper registry
0. Install and run zookeeper in localhost:

Linux:
```sh
cd ~
wget http://www.apache.org/dist//zookeeper/zookeeper-3.4.9/zookeeper-3.4.9.tar.gz
tar zxvf zookeeper-3.3.3.tar.gz
cd zookeeper-3.3.3/conf
cp zoo_sample.cfg zoo.cfg
vi zoo.cfg
- edit: dataDir=/home/zookeeper/data
cd ../bin
./zkServer.sh start
```

Windows:
```sh
cd ~
Chrome download http://www.apache.org/dist//zookeeper/zookeeper-3.4.9/zookeeper-3.4.9.tar.gz
unzip zookeeper-3.3.3.tar.gz
cd zookeeper-3.3.3/conf
copy zoo_sample.cfg zoo.cfg
open zoo.cfg
- edit: dataDir=c:\zookeeper\data
cd ../bin
zkServer.cmd start
```
0. change registry setting in config files:

```sh
* ${basedir}/dubbo-demo/dubbo-demo-provider/src/main/resources/META-INF/spring/dubbo-demo-provider.xml
* ${basedir}/dubbo-demo/dubbo-demo-consumer/src/main/resources/META-INF/spring/dubbo-demo-consumer.xml
edit config '<dubbo:registry address="zookeeper://127.0.0.1:2181"/>'
* ${basedir}/dubbo-simple/dubbo-monitor-simple/src/test/resources/dubbo.properties
edit config 'dubbo.registry.address=zookeeper://127.0.0.1:2181'
```
0. restart  Demo:
```sh
 DemoProvider.java run main method
 DemoConsumer.java run main method
 SimpleMonitor.java run main method
 chrome open http://127.0.0.1:8080
```

## Demo Scenario4: redis registry
0. Install and run redis in localhost:

Linux:
```sh
cd ~
wget http://download.redis.io/releases/redis-3.2.5.tar.gz
tar xzf redis-3.2.5.tar.gz
cd redis-3.2.5
make
cd 
vi redis.conf
--edit: find '# requirepass foobared' change to  'requirepass abc123'
nohup ./src/redis-server redis.conf &
```

Windows:
```sh
Chrome download https://github.com/MSOpenTech/redis/releases/download/win-3.2.100/Redis-x64-3.2.100.zip
unzip Redis-x64-3.2.100.zip
cd Redis-x64-3.2.100
open redis.windows.conf
--edit: find '# requirepass foobared' change to  'requirepass abc123'
cd Redis-x64-3.2.100
redis-server.exe redis.windows.conf
```
0. change registry setting in config files:

```sh
* ${basedir}/dubbo-demo/dubbo-demo-provider/src/main/resources/META-INF/spring/dubbo-demo-provider.xml
* ${basedir}/dubbo-demo/dubbo-demo-consumer/src/main/resources/META-INF/spring/dubbo-demo-consumer.xml
edit config '<dubbo:registry address="redis://127.0.0.1:6379"/>'
* ${basedir}/dubbo-simple/dubbo-monitor-simple/src/test/resources/dubbo.properties
edit config 'dubbo.registry.address=redis://127.0.0.1:6379'
```
0. restart  Demo:
```sh
 DemoProvider.java run main method
 DemoConsumer.java run main method
 SimpleMonitor.java run main method
 chrome open http://127.0.0.1:8080
```


## Install the admin console:

```sh
--Start zookeeper
cd ~/dubbo/dubbo-admin
mvn jetty:run -Ddubbo.registry.address=zookeeper://127.0.0.1:2181
http://root:root@127.0.0.1:8080
```
