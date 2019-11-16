# Ubuntu 安装samba
## 命令安装
```shell
sudo apt-get install samba openssh-server
```
## 修改配置(/etc/samba/smb.conf)
```shell
[homes]
   comment = Home Directories
   browseable = yes
# By default, the home directories are exported read-only. Change the
# next parameter to 'no' if you want to be able to write to them.
   read only = no
# File creation mask is set to 0700 for security reasons. If you want to
# create files with group=rw permissions, set next parameter to 0775.
   create mask = 0755 #建议将权限修改成0755，这样其它用户只是不能修改
# Directory creation mask is set to 0700 for security reasons. If you want to
# create dirs. with group=rw permissions, set next parameter to 0775.
   directory mask = 0755
# By default, \\server\username shares can be connected to by anyone
# with access to the samba server. Un-comment the following parameter
# to make sure that only "username" can connect to \\server\username
# The following parameter makes sure that only "username" can connect
#
# This might need tweaking when using external authentication schemes
   valid users = %S #本行需要取消注释
```

## 重启samba服务
```shell
sudo service restart smbd
sudo service restart nmbd
```

## 增加一个现有用户的对应samba帐号
```shell
sudo smbpasswd -a lines
# 根据提示输入两次密码即可
```

## 登录,Window下输入samba地址尝试登录
```
\\10.0.0.2\lines
```