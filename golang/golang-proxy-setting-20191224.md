# 设置golang下载代理
* 由于国内限制，无法访问 [golang.org](https://golang.org), 导致无法下载[golang.org/x/](https://golang.org/x/)目录下的packages
* 为了解决这个问题，有两种方法可以解决：

## 1. 从GitHub上下载

golang.org/x/text 对应 github.com/golang/text
```shell
mkdir $GOPATH/src/golang.org/x
cd $GOPATH/src/golang.org/x
git clone git@github.com:golang/text.git
rm -rf text/.git
```
## 2. 设置代理
```shell
https://goproxy.io/
export GOPROXY=https://goproxy.io
```

## 参考:
[一键解决 go get golang.org/x 包失败](https://segmentfault.com/a/1190000018264719)   
[goproxy.io](https://goproxy.io/)
