zookeeper集群

一.zookeeper集群部署

下载：http://archive.apache.org/dist/zookeeper/ \
集群版本： apache-zookeeper-3.5.8-bin.tar.gz
 
#### 机器1： ip: 81.140.12.51

1.解压 tar -zxvf apache-zookeeper-3.5.8-bin.tar.gz \
2.cd apache-zookeeper-3.5.8-bin/    \
3.cp -r conf/zoo_sample.cfg  zoo.cfg \
4.vim zoo.cfg \
5.新增配置 \
quorumListenOnAllIPs=true       \
server.1=9.140.12.51:2888:3888      \
server.2=122.4.81.175:2888:3888     \
server.3=106.14.137.230:2888:3888 \
dataDir=/apache-zookeeper-3.5.8-bin/data \
6.创建data文件夹  
cd /apache-zookeeper-3.5.8-bin   \
mkdir data  \
7.创建myid文件 \
vim myid
机器id ---》1
最终文件值只为1

8.进入到bin目录后，启动zk \
sh zkServer.sh  start ../conf/zoo.cfg
 
#### 机器2： ip: 122.4.81.175

1.解压 tar -zxvf apache-zookeeper-3.5.8-bin.tar.gz \
2.cd apache-zookeeper-3.5.8-bin/    \
3.cp -r conf/zoo_sample.cfg  zoo.cfg    \
4.vim zoo.cfg   \
5.新增配置  \
quorumListenOnAllIPs=true       \
server.1=9.140.12.51:2888:3888      \
server.2=122.4.81.175:2888:3888     \
server.3=106.14.137.230:2888:3888   \
dataDir=/apache-zookeeper-3.5.8-bin/data    \
6.创建data文件夹     \
cd /apache-zookeeper-3.5.8-bin  
mkdir data  \
7.创建myid文件  \
vim myid
机器id ---》2
最终文件值只为2

8.进入到bin目录后，启动zk    \
sh zkServer.sh  start ../conf/zoo.cfg

#### 机器3： ip: 106.14.137.230

1.解压 tar -zxvf apache-zookeeper-3.5.8-bin.tar.gz    \
2.cd apache-zookeeper-3.5.8-bin/    \
3.cp -r conf/zoo_sample.cfg  zoo.cfg    \
4.vim zoo.cfg   \
5.新增配置      \
quorumListenOnAllIPs=true       \
server.1=9.140.12.51:2888:3888      \
server.2=122.4.81.175:2888:3888     \
server.3=106.14.137.230:2888:3888       \
dataDir=/apache-zookeeper-3.5.8-bin/data    \
6.创建data文件夹     \
cd /apache-zookeeper-3.5.8-bin      \
mkdir data  \
7.创建myid文件  \
vim myid
机器id ---》3
最终文件值只为3

8.进入到bin目录后，启动zk    \
sh zkServer.sh  start ../conf/zoo.cfg

 
#### 检查集群是否启动成功 
机器1.    \
sh zkServer.sh status   \
Using config: /home/wph/apache-zookeeper-3.5.8-bin/bin/../conf/zoo.cfg  \
Client port found: 2181. Client address: localhost. \
Mode: follower

机器2.    \
sh zkServer.sh status   \
ZooKeeper JMX enabled by default    \
Using config: /home/wph/apache-zookeeper-3.5.8-bin/bin/../conf/zoo.cfg  \
Client port found: 2181. Client address: localhost.
Mode: follower

机器3.\
sh zkServer.sh status \
ZooKeeper JMX enabled by default    \
Using config: /home/wph/apache-zookeeper-3.5.8-bin/bin/../conf/zoo.cfg  \
Client port found: 2181. Client address: localhost. \
Mode: leader






