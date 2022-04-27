---
title: Docker使用

---



1.创建镜像

```
docker login
docker pull centos:7
```

2.运行容器

```
docker run -itd --net=host 镜像ID(IMAGE ID) /bin/bash
```

3.启动容器

```
docker start  容器id
```

4.进入容器

```
docker exec -it 容器ID(CONTAUNER ID)  bash
```

5.安装网络工具和ssh

```
yum install -y net-tools
yum install openssh
yum -y install openssh-clients
yum install openssh-server
```

6.关闭容器

```
docker stop 容器名称
```

7.提交

```
docker commit 容器ID 镜像名:latest
```

8.查看镜像

```
docker images
```

9.查看容器

```
docker ps
```

