# Git使用

## git基本操作

```shell
## 克隆远程仓库到本地
git clone 远程仓库地址 (localDirectory)

## 初始化仓库
git init 

## 添加文件到暂存区
git add .

##  将暂存区内容添加到仓库中。
git commit -m"XXX"
git commit

## 如果是本地项目推到远程仓库需要执行以下命令
git remote add origin 仓库地址

## 将暂存区内容推到origin上
git push origin 自己的开发分支

## 删除分支 本地/远程
git branch -d 分支
git push origin --delete Chapater6

## 查看所有分支（包括远程）
git branch -a
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



## git回退版本

```shell
## 1.寻找需要回退到之前的版本号
git log

## 2.使用reset或者revert将版本回退
git reset --hard 版本号
git revert -n 版本号

## 3.强制push到对应的远程分支（如提交到develop分支）
git push -f -u origin develop

## 3.提交并推送远程分支。通知其他人更新代码
git commit -m XXX
git push

## 通过reset的方式，把head指针指向之前的某次提交，reset之后，后面的版本就找不到了

## revert不会把版本往前回退，而是生成一个新的版本。所以，你只需要让别人更新一下代码就可以了，你之前操作的提交记录也会被保留下来
```

