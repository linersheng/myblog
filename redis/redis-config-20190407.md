# Redis 常用配置 #
```shell
#配置密码
requirepass xxx

#关闭只能本地访问,把改行注释
#bind 127.0.0.1

#关闭包含模式
protected-mode no

#expire订阅
notify-keyspace-events "KEx"

```

## 参考资料 ##
[Redis系列—Redis事件订阅](https://blog.csdn.net/u012758088/article/details/77285499)
