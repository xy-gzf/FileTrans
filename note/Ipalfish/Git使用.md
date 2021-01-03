# Git使用

## git基本操作

```shell
## git init - 初始化仓库。

## git add . - 添加文件到暂存区。

## git commit - 将暂存区内容添加到仓库中。
```



## merge冲突解决

```shell
##1. 本地执行git checkout master命令，切换分支至master
git checkout master

##2. 执行git pull --rebase命令，拉取master最新代码
git pull --rebase

##3. 本地执行git checkout 你的开发分支 命令，切换到你的开发分支
git checkout 你的开发分支

##4. 执行git merge master命令，将master代码合并到你的开发分支，此时可能会有代码冲突，本地将代码冲突解决
git merge master

##5. 代码冲突解决完毕后，将代码push到你的远程开发分支
git push origin ...

##6. 重新创建merge request即可，如还有冲突，重复1-5步

```



