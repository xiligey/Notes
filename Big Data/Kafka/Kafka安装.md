## Win10下安装Kafka

### 安装

1、官网下载[http://kafka.apache.org/downloads.html](http://kafka.apache.org/downloads.html)

2、解压到C盘根目录下（Kafka路径太长会报错：输入行太长。命令语法不正确。）

3、修改config目录下的server.properties

`log.dirs=C:\kafka_2.12-3.1.0\logs`

### 启动

4、启动zk

```bash
C:\Users\chenxilin\Install\BigData\Kafka\bin\windows\zookeeper-server-start.bat C:\Users\chenxilin\Install\BigData\Kafka\config\zookeeper.properties
```

5、启动kafka

```bash
C:\Users\chenxilin\Install\BigData\Kafka\bin\windows\kafka-server-start.bat C:\Users\chenxilin\Install\BigData\Kafka\config\server.properties
```



`C:\kafka_2.12-3.1.0\bin\windows\kafka-server-start.bat C:\kafka_2.12-3.1.0\config\server.properties`

## Linux下安装Kafka

1、下载

`wget https://dlcdn.apache.org/kafka/3.1.0/kafka_2.12-3.1.0.tgz`

[`wget https://dlcdn.apache.org/kafka/3.3.1/kafka_2.13-3.3.1.tgz`](https://dlcdn.apache.org/kafka/3.3.1/kafka_2.13-3.3.1.tgz)

2、添加环境变量

`vim ~/.bashrc`

```bash
export KAFKA_HOME=/home/chenxilin/Install/Kafka/kafka_2.12-3.1.0
export PATH=/home/chenxilin/Install/Kafka/kafka_2.12-3.1.0/bin
```

## Mac下安装Kafka

MacOS 上可以方便的使用 `brew` 进行安装。

### 安装

如果还没有安装`Java`, 可以先安装Java: `brew cask install java`

然后安装`zookeeper`和`kafka`。

```bash
brew install kafka
brew install zookeeper
```

修改 `/usr/local/etc/kafka/server.properties`, 找到 `listeners=PLAINTEXT://:9092` 那一行，把注释取消掉。然后修改为:

```bash
############################# Socket Server Settings #############################
# The address the socket server listens on. It will get the value returned from 
# java.net.InetAddress.getCanonicalHostName() if not configured.
#   FORMAT:
#     listeners = listener_name://host_name:port
#   EXAMPLE:
#     listeners = PLAINTEXT://your.host.name:9092
listeners=PLAINTEXT://localhost:9092
```

### 启动

如果想以服务的方式启动，那么可以:

```bash
$ brew services start zookeeper
$ brew services start kafka
```

如果只是临时启动，可以:

```bash
$ zookeeper-server-start ../config/zookeeper.properties
$ kafka-server-start ../config/server.properties
```