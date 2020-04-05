# Git常用命令

```
#配置用户信息
git config --global user.email "xxx@qq.com"
git config --global user.name "xxx"

#拉取服务代码
git clone https://github.com/linersheng/gelian.git

#添加本地文件
git add ./

#获取当前状态
git status

#提交代码
git commit -m "first time upload"

#推送到服务器
git push

#更新本地代码
git pull

#储藏工作内容
git stash

#查看现有的储藏
git stash list

#恢复储藏
git stash apply stash@{2}

#删除储藏
git stash drop stash@{0}

```

### 网络篇
[Pro Git（中文版）](https://gitee.com/progit/)