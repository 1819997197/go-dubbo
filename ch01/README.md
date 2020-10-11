## zookeeper简介以及安装

#### 一、zookeeper简介
```
ZooKeeper 是一个开源的分布式协调服务，一个典型的分布式数据一致性解决方案。分布式应用程序可以基于 ZooKeeper 实现诸如数据发布/订阅、负载均衡、命名服务、分布式协调/通知、集群管理、Master 选举、分布式锁和分布式队列等功能.

简单来说zookeeper=文件系统+监听通知机制。
```

#### 二、单机模式安装
```
1.下载ZooKeeper，地址 http://mirrors.hust.edu.cn/apache/zookeeper/

2.解压到安装目录 tar -zxvf apache-zookeeper-3.6.2-bin.tar.gz -C /usr/local/

3.进入conf目录，创建一个zookeeper的配置文件zoo.cfg，可复制conf/zoo_sample.cfg作为配置文件

4、可以不修改zoo.cfg，默认配置就行，进去zookeeper安装目录，启动ZooKeeper
启动命令：./bin/zkServer.sh start
停止命令：./bin/zkServer.sh stop　　
重启命令：./bin/zkServer.sh restart
状态查看命令：./bin/zkServer.sh status
```

#### 三、验证
1.启动zookeeper
```
[vagrant@localhost apache-zookeeper-3.6.2-bin]$ sudo ./bin/zkServer.sh start
/usr/bin/java
ZooKeeper JMX enabled by default
Using config: /usr/local/apache-zookeeper-3.6.2-bin/bin/../conf/zoo.cfg
Starting zookeeper ... STARTED
```

2.查看服务状态
```
[vagrant@localhost apache-zookeeper-3.6.2-bin]$ ./bin/zkServer.sh status
/usr/bin/java
ZooKeeper JMX enabled by default
Using config: /usr/local/apache-zookeeper-3.6.2-bin/bin/../conf/zoo.cfg
Client port found: 2181. Client address: localhost. Client SSL: false.
Mode: standalone

// 启动之后如果能看到Mode:standalone就表示启动成功了
```

#### 四、CURD
1.使用客户端连接ZooKeeper服务
```
./bin/zkCli.sh -server 127.0.0.1:2181
// 会出现Welcome to ZooKeeper!
```

2.查看客户端命令帮助
```
[zk: 127.0.0.1:2181(CONNECTED) 0] help
```

3.创建了一个新的 znode 节点"zk"以及与它关联的字符串
```
[zk: 127.0.0.1:2181(CONNECTED) 1] create /zk dubbo
Created /zk
```

4.使用 ls 命令来查看当前 ZooKeeper 中所包含的内容
```
[zk: 127.0.0.1:2181(CONNECTED) 0] ls /
[zk, zookeeper]
```

5.获取znode节点"zk"
```
[zk: 127.0.0.1:2181(CONNECTED) 3] get /zk
dubbo
```

6.删除znode节点"zk"
```
[zk: 127.0.0.1:2181(CONNECTED) 10] delete /zk
[zk: 127.0.0.1:2181(CONNECTED) 11] ls /
[zookeeper]
```

7.退出客户端
```
[zk: 127.0.0.1:2181(CONNECTED) 12] quit
```
