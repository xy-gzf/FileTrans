# Map



## 声明

var map变量名 map[keytype]valuetype

- **类型**

```text
Key类型：
	可以使用int、string、map、channel、bool
	
Value类型：
	和Key基本一样
	
通常为int、string
key不能使用slice、map、func，因为无法用于==判断
	
var a map[string]string
var a map[int]int
var a map[int]string
var a map[string]map[string]string
```

- <a style="color:red">**注意**</a>

  声明是不会分配内存的，初始化需要make，分配内存后才能赋值和使用

```go
var a map[string]string
a = make(map[string]string, 10)
a["1"] = "abc"
```



## 遍历

```go
//使用for range
var a map[string]string
a = make(map[string]string, 10)
a["1"] = "zs"
a["2"] = "zs"
for key,val := range a {
  fmt.Printf("key = %s , val = %s\n",key,val)
}
```



## map切片

```go
//map切片
var mlice []map[string]string
mlice = make([]map[string]string,2)
if mlice[0] == nil {
  mlice[0] = make(map[string]string , 2)
  mlice[0]["name"] = "zs"
  mlice[0]["age"] = "19"
}
if mlice[1] == nil {
  mlice[1] = make(map[string]string , 2)
  mlice[1]["name"] = "ls"
  mlice[1]["age"] = "20"
}

var newlice map[string]string
newlice = make(map[string]string , 1)
newlice["name"] = "ww"
newlice["age"] = "14"

mlice = append(mlice,newlice)

fmt.Println(mlice)

//动态追加需要使用append函数，追加下标大于开辟大小则会下标越界
```

