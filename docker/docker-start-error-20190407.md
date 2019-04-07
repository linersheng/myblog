# Docker 启动容器报错(命名冲突) #

运行：
docker run -d -p 6379:6379 --name="myredis" redis redis-server --appendonly yes

错误提示：
docker: Error response from daemon: Conflict. The container name "/myredis" is already in use by container "8fc922fba65f7d720c56f5b12bde8588ff3adb1303eb2abf7c7c1dce03bb0b65". You have to remove (or rename) that container to be able to reuse that name.
See 'docker run --help'.

通过docker ps -a查看，之前启动过该容器，出现命名冲突了，直接使用docker restart myredis即可启动。
