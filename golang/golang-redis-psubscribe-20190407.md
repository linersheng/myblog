# Golang实现redis的订阅 #

## 功能需求 ##
* 记录用户登录和登出的时间
* 统计当前用户是否在线

## 思路 ##
1. 用户id和登录时间作为key，即id:time   
2. 每次心跳就更新expire的时间   
3. 订阅所有key的超时时间，并写入日志

## 代码实现 ##
```golang
import (
    "fmt"
    "github.com/gomodule/redigo/redis"
    )

func subscribe() {
	c := pool.Get()
    defer c.Close()
	c.Send("PSUBSCRIBE", "__keyevent@0__:*")
	c.Flush()
	for {
		reply,err := c.Receive() 
		if err != nil {
			fmt.Println("recive err:", err)
			return
		}
		vacs, ok := reply.([]interface{})
		if ok {
			for _, r := range vacs {
				if v, ok := r.([]uint8); ok {
					fmt.Println("[]byte value:", string(v))
				} else if v, ok := r.(int64); ok{
					fmt.Println("int value:", v)
				}else {
					fmt.Printf("convert to string fail.(%v)\n", r)
				}
				fmt.Println(reflect.TypeOf(r))
			}
		} else {
			fmt.Println("convert to [] interface{} fail.")
		}
	}
}
```

## 遇到问题 ##
1. 接收不到超时事件
 修改配置文件，设置"notify-keyspace-events Kex"   
 测试可以参考 [Redis系列—Redis事件订阅](https://blog.csdn.net/u012758088/article/details/77285499)   

2. 不知道c.Receive()返回的reply是什么类型   
  通过fmt.Println(reflect.TypeOf(reply))得知是[]interface{}类型  

3. 如何解析数据，是否可以拿到key和value   
  官方给的另一种写法，已经解析好数据，但是没拿到value   
```golang
//Example1：
c.Send("SUBSCRIBE", "example")
c.Flush()
for {
    reply, err := c.Receive()
    if err != nil {
        return err
    }
    // process pushed message
}

//Example2：
psc := redis.PubSubConn{Conn: c}
psc.Subscribe("example")
for {
    switch v := psc.Receive().(type) {
    case redis.Message:
        fmt.Printf("%s: message: %s\n", v.Channel, v.Data)
    case redis.Subscription:
        fmt.Printf("%s: %s %d\n", v.Channel, v.Kind, v.Count)
    case error:
        return v
    }
}
```
  尝试直接写代码接解析，遇到不知道的类型，就用反射来打印。看了psc.Receive()方法，实现起来很复杂，所以还是自己来做转换出来快,看了源码，才知道拿不到value.

4. 如何判断接收到的消息是什么类型
```shell
[]byte value: psubscribe
[]byte value: __keyspace@0__:*
int value: 1
[]byte value: psubscribe
[]byte value: __keyevent@0__:*
int value: 2
[]byte value: pmessage
[]byte value: __keyspace@0__:*
[]byte value: __keyspace@0__:lines
[]byte value: expired
```
reply.([]interface{})转换出来的第一个值就是消息的类型， **psubscribe** 、**pmessage** 就是消息的第一个值。

