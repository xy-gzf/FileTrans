# Pub



## thrift

*版本 0.9.2*

```shell
## 使用thrift之前需要先使配置生效
source ~/.bash_profile

## 使用thrift生成命令
thrift -I ../../util_thrift/idl -gen go:package_prefix=code.ibanyu.com/server/go/util.git/idl/gen-go/ Xxx.thrift

../../../util/idl 当前电脑绝对路径为：/Users/zhaofanguo/go/util_thrift/idl
```

修改完成后需要对Adapter内函数进行相应修改，增加时需要手动添加一个func



## grpc



```shell
## 使用protoc生成

protoc -I=. -I=/Users/zhaofanguo/go/util_thrift/idl/ --go_out=plugins=grpc:./grpc/talentarchive TalentArchive.proto
```
