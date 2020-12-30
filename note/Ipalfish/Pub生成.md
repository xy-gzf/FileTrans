# Pub



## thrift

*版本 0.9.2*



```shell
//使用thrift生成命令
thrift -I ../../../util/idl -gen go:package_prefix=code.ibanyu.com/server/go/util.git/idl/gen-go/ Xxx.thrift

../../../util/idl 当前电脑绝对路径为：/Users/zhaofanguo/go/util_thrift/idl
```





## grpc



```shell
//使用protoc生成

protoc -I=. -I=/Users/zhaofanguo/go/util_thrift/idl/ --go_out=plugins=grpc:./grpc/talentarchive TalentArchive.proto
```
