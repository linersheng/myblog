# 启动容器，提示端口转发错误

```shell
docker run -d -p 6379:6379 --name "myredis" redis redis-server  --appendonly yes

docker: Error response from daemon: driver failed programming external connectivity on endpoint myredis (d13048224958a6b6db955b63995869a9f38a160d76dee7b2b1ca1c8bae8f28c5): Error starting userland proxy: mkdir /port/tcp:0.0.0.0:6379:tcp:172.17.0.2:6379: input/output error.
```

## 解决方法
重启docker

## 原因
* 启动docker后，网络发生了变化，电脑和路由器断开了
* 在电脑的网络发生变化后，需要重启docker