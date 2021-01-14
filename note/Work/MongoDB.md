# MongoDB



## 数据库

```mysql
## 创建数据库（如果数据库不存在，创建数据库，否则切换至指定数据库）
use Database_NAME

## 查看数据库
show dbs

## 删除数据库（切换至需删除的数据库）
db.dropDatabase()

```



## 集合

```mysql
## 创建集合 
## options: 可选参数, 指定有关内存大小及索引的选项
db.createCollection(name, options)


## 在 MongoDB 中，你不需要创建集合。当你插入一些文档时，MongoDB 会自动创建集合。
> db.mycol2.insert({"name" : "自动创建集合"})
> show collections
mycol2


## 删除集合
db.collection.drop()
>db.mycol2.drop()
true
>


```



## 文档

- **插入文档**

    ```mysql
    ## MongoDB 使用 insert() 或 save() 方法向集合中插入文档，语法如下：
    db.COLLECTION_NAME.insert(document)
    或
    db.COLLECTION_NAME.save(document) ## 新版本已废弃
    ## insert如果主键存在则会抛出异常、提示主键重复
    ```

    新增方法

    ```mysql
    ## db.collection.insertOne() 用于向集合插入一个新文档，语法格式如下：
    db.collection.insertOne(
       <document>,
       {
          writeConcern: <document>
       }
    )
    
    
    ## db.collection.insertMany() 用于向集合插入一个多个文档，语法格式如下：
    db.collection.insertMany(
       [ <document 1> , <document 2>, ... ],
       {
          writeConcern: <document>,
          ordered: <boolean>
       }
    )
    
    -- document：要写入的文档。
    -- writeConcern：写入策略，默认为 1，即要求确认写操作，0 是不要求。
    -- ordered：指定是否按顺序写入，默认 true，按顺序写入。
    ```

- 