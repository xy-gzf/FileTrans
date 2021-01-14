# Go

## 包package

打包及使用包内

```go
//main函数文件
package main

/*
	导入包，路径这里从GOPATH路径下src下开始。
	支持给包起别名，但起别名之后只能使用别名
*/
import "util"	

func main(){
  //引用util包内的Call函数
  util.Call()
}


//util包内Call函数文件

/*
	这里将该文件内函数进行打包，然后在调用函数的文件内导入包即可
 */
package util

import "fmt"

func Call(){
  fmt.Println("This is util Call...")
}
```

## defer关键字

#### 用法

```go
func deferFunc(a int){
    defer fmt.Println(a)
    a++;
    defer fmt.Println(a)
}

func main(){
    deferFunc(10)    
}

//输出结果
//11
//10
```

1. go语言执行到一个defer时，并不会直接执行其代码，而是将执行放入到栈内， 等函数执行完毕才会从栈中取出执行结果

**注意**

defer将语句入栈时，会将相关的值拷贝入栈

#### defer的价值

**当函数执行完，可以及时释放函数创建的资源**

```go
func test(){
    //关闭文件资源
    file = openfile(文件名)
    defer file.close()
    //其他代码
}
```

## 函数参数传递

 不管时值传递还是引用传递，在函数传递过程中都是变量的副本，值传递是值的副本，引用传递是地址的副本。 

- **值传递**

  基本数据类型（包括string）、数组、结构体struct

- **引用传递**

  指针、切片slice、map、管道chan、interface



## 变量作用域

- **局部变量**

  函数内部定义的变量，不管大小写都是只能内部使用

- **全局变量**

  函数外定义的变量，首字母小写在整个包内有效，大写则在整个程序中有效 

- **代码块**

  If/for代码块中只在代码块中有用

