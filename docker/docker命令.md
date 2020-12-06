##### docker常用命令



```
docker images : 列出本地镜像
docker pull : 从镜像仓库中拉取或者更新指定镜像

docker run ：创建一个新的容器并运行一个命令
-d: 后台运行容器，并返回容器ID
-p: 端口映射，格式为：主机(宿主)端口:容器端口
--name="nginx-lb": 为容器指定一个名称
-v：目录映射，格式为：主机目录:容器目录

docker rm ：删除一个或多个容器
docker start :启动一个或多少已经被停止的容器
docker stop :停止一个运行中的容器
docker kill :杀掉一个运行中的容器（强制）
docker restart :重启容器
docker port :列出指定的容器的端口映射，或者查找将PRIVATE_PORT NAT到面向公众的端口。

docker logs : 获取容器的日志
-f : 跟踪日志输出
--since :显示某个开始时间的所有日志
-t : 显示时间戳
--tail :仅列出最新N条容器日志

docker exec -i -t  mynginx /bin/bash：在容器mynginx中开启一个交互模式的终端，即通过SSH协议进入容器

docker ps : 列出容器
-a :显示所有的容器，包括未运行的。

docker cp：拷贝主机docker cp /www/runoob 96f7f14e99ab:/www/
```



docker启动mysql

```
docker run --name mysql01 -e MYSQL_ROOT_PASSWORD=root -p 3306:3306 -d mysql:5.7.21
```

