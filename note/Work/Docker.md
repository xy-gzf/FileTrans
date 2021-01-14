## Docker



```shell
## 查看本地镜像
docker images

## 查看容器运行信息
docker ps

## 运行容器
docker run -itd --name mongo -p 27017:27017 mongo --auth
docker run -itd --name redis-test -p 6379:6379 redis

## 进入容器
docker exec -it mongo mongo admin
docker exec -it redis-test /bin/bash

## 连接容器
db.auth('admin', '123456')
redis-cli

## 分别为mongo及redis的连接使用方式
```

