# hadoop

## 1、容器网络

> master: 172.17.0.2
> slave1: 172.17.0.3
> slave2: 172.17.0.4

## 2、hadoop集群使用介绍

> 构建cluster-hadoop镜像
> docker build -t  cluster-hadoop ./
> hadoop 单机的集群，以 centos-base 为基础镜像。

## 3、hadoop docker方式启动集群

```bash
docker network create --subnet=172.18.0.0/16 hadoop-network
docker run -itd --name hadoop-master --hostname=hadoop-master --net hadoop-network --ip 172.18.0.2 cluster-hadoop
docker run -itd --name hadoop-slave1 --hostname=hadoop-slave1 --net hadoop-network --ip 172.18.0.3 cluster-hadoop
docker run -itd --name hadoop-slave2 --hostname=hadoop-slave2 --net hadoop-network --ip 172.18.0.4 cluster-hadoop
```

## 4、hadoop docker-compose方式启动集群

```bash
docker-compose up -d
```
