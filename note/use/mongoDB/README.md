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



mongoDB对应sql的概念

| SQL术语/概念 | MongoDB术语/概念 | 解释/说明                           |
| :----------- | :--------------- | :---------------------------------- |
| database     | database         | 数据库                              |
| table        | collection       | 数据库表/集合                       |
| row          | document         | 数据记录行/文档                     |
| column       | field            | 数据字段/域                         |
| index        | index            | 索引                                |
| table joins  |                  | 表连接,MongoDB不支持                |
| primary key  | primary key      | 主键,MongoDB自动将_id字段设置为主键 |

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

#### 插入文档

```mysql
## MongoDB 使用 insert() 或 save() 方法向集合中插入文档，语法如下：
db.COLLECTION_NAME.insert(document)
或
db.COLLECTION_NAME.save(document) ## 新版本已废弃
## insert如果主键存在则会抛出异常、提示主键重复
```

- 新增方法

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

- 插入示例

    ```mysql
    ## 直接插入
    db.col.insert({title: 'MongoDB 教程', 
        description: 'MongoDB 是一个 Nosql 数据库',
        by: '菜鸟教程',
        url: 'http://www.runoob.com',
        tags: ['mongodb', 'database', 'NoSQL'],
        likes: 100
    })
    
    
    
    ## 将数据定义为一个变量，插入变量
    document=({title: 'MongoDB 教程', 
        description: 'MongoDB 是一个 Nosql 数据库',
        by: '菜鸟教程',
        url: 'http://www.runoob.com',
        tags: ['mongodb', 'database', 'NoSQL'],
        likes: 100
    });
    
    db.col.insert(document)
    ```



#### 更新文档

- Update()方法

    ```mysql
    db.collection.update(
       <query>,
       <update>,
       {
         upsert: <boolean>,
         multi: <boolean>,
         writeConcern: <document>
       }
    )
    ```
    
    - **query** : update的查询条件，类似sql update查询内where后面的。
    - **update** : update的对象和一些更新的操作符（如$,$inc...）等，也可以理解为sql update查询内set后面的
    - **upsert **: 可选，这个参数的意思是，如果不存在update的记录，是否插入objNew,true为插入，默认是false，不插入。
    - **multi** : 可选，mongodb 默认是false,只更新找到的第一条记录，如果这个参数为true,就把按条件查出来多条记录全部更新。
    - **writeConcern** :可选，抛出异常的级别。
    
- 示例

    ```mysql
    db.col.update({'title':'MongoDB 教程'},{$set:{'title':'MongoDB'}})
    
    ## 可以看到标题(title)由原来的 "MongoDB 教程" 更新为了 "MongoDB"。
    ## 以上语句只会修改第一条发现的文档，如果你要修改多条相同的文档，则需要设置 multi 参数为 true。
    
    db.col.update({'title':'MongoDB 教程'},{$set:{'title':'MongoDB'}},{multi:true})
    ```



#### 删除文档

- remove()方法

    ```mysql
    db.collection.remove(
       <query>,
       {
         justOne: <boolean>,
         writeConcern: <document>
       }
    )
    
    ```

    - **query** :（可选）删除的文档的条件。
    - **justOne** : （可选）如果设为 true 或 1，则只删除一个文档，如果不设置该参数，或使用默认值 false，则删除所有匹配条件的文档。
    - **writeConcern** :（可选）抛出异常的级别。

- 示例

    ```mysql
    db.col.remove({'title':'MongoDB 教程'})
    
    
    ## 只想删除第一条找到的记录可以设置 justOne 为 1，如下所示：
    db.COLLECTION_NAME.remove(DELETION_CRITERIA,1)
    
    
    ## 删除所有数据，可以使用以下方式（类似常规 SQL 的 truncate 命令）：
    db.col.remove({})
    ```

    

#### 查询文档

- 查询语法

    ```mysql
    db.collection.find(query, projection)
    
    
    ## 如果你需要以易读的方式来读取数据，可以使用 pretty() 方法，语法格式如下：
    db.col.find().pretty()
    ```

    - **query** ：可选，使用查询操作符指定查询条件
    - **projection** ：可选，使用投影操作符指定返回的键。查询时返回文档中所有键值， 只需省略该参数即可（默认省略）。

- 示例

    ```mysql
     db.col.find().pretty()
     
    ## 除了 find() 方法之外，还有一个 findOne() 方法，它只返回一个文档。
    ```

- and条件

    ```mysql
    ## MongoDB 的 find() 方法可以传入多个键(key)，每个键(key)以逗号隔开，即常规 SQL 的 AND 条件。
    
    db.col.find({key1:value1, key2:value2}).pretty()
    ```

- or条件

    ```mysql
    ## MongoDB OR 条件语句使用了关键字 $or,语法格式如下：
    db.col.find(
       {
          $or: [
             {key1: value1}, {key2:value2}
          ]
       }
    ).pretty()
    ```



#### 条件操作符

| 操作       | 格式                     | 范例                                        | DB中类似语句            |
| :--------- | ------------------------ | ------------------------------------------- | ----------------------- |
| 等于       | `{<key>:<value>`}        | `db.col.find({"by":"菜鸟教程"}).pretty()`   | `where by = '菜鸟教程'` |
| 小于       | `{<key>:{$lt:<value>}}`  | `db.col.find({"likes":{$lt:50}}).pretty()`  | `where likes < 50`      |
| 小于或等于 | `{<key>:{$lte:<value>}}` | `db.col.find({"likes":{$lte:50}}).pretty()` | `where likes <= 50`     |
| 大于       | `{<key>:{$gt:<value>}}`  | `db.col.find({"likes":{$gt:50}}).pretty()`  | `where likes > 50`      |
| 大于或等于 | `{<key>:{$gte:<value>}}` | `db.col.find({"likes":{$gte:50}}).pretty()` | `where likes >= 50`     |
| 不等于     | `{<key>:{$ne:<value>}}`  | `db.col.find({"likes":{$ne:50}}).pretty()`  | `where likes != 50`     |

