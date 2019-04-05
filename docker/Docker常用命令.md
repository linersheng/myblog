# Docker常用命令
---
```shell
#拉取容器，即从服务器下载容器到本地
docker pull hello-world

#运行容器
docker run -d -p 1234:1234 --name="mydocker" hello-world

#查看正在运行的容器
docker ps 

#查看所有容器，包括正在运行的和已经停止的
docker ps -a

#重新启动容器（运行docker run hello-world --name="mydocker"后，要么重启容器，要么先删除容器再次执行)
docker restart xxx
```