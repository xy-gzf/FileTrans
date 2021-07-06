## Docker



```shell
## 查看本地镜像
docker images

## 查看容器运行信息
docker ps

## 运行容器
docker run -itd --name mongo -p 27017:27017 mongo --auth
docker run -itd --name redis -p 6379:6379 redis
# docker run --name=redis --detach=true --publish=6379:6379 redis
docker start (container id)

## 进入容器
docker exec -it mongo mongo admin
docker exec -it redis /bin/bash

## 连接容器
db.auth('admin', '123456')
redis-cli

## 分别为mongo及redis的连接使用方式

## 操作方式链接
https://www.runoob.com/docker/docker-container-usage.html
```



```shell
## 启动容器
docker start CONTAINER

## 停止运行的容器
docker stop CONTAINER

## 重启容器
dokcer restart CONTAINER

```

**Docker命令大全**

https://www.runoob.com/docker/docker-command-manual.html