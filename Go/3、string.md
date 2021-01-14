# string函数库



## string常用函数

1. **长度** 

   ```go
   //按字节长度计算
   str := "hello北京"
   n := len(str)
   //n 为 11
   ```

2. **字符串遍历** 

   ```go
   //遍历r可解决字符串中中文遍历的问题
   str := "hello北京"
   r := []rune(str)
   for i := 0 ; i < len(r) ; i++ {
     fmt.printf("= %c \n",r[i])
   }
   //直接遍历str  中文会出错
   ```

3. **字符串转整数**

   ```go
   //str不能转为整数的话则err不为nil，转换失败
   n , err := strconv.Atoi("123")
   if err != nil {
     fmt.Println("转换失败")
   } else {
     fmt.Printf("n type is %T , n = %v\n", n , n)
   }
   ```

4. **整数转字符串 **

   ```go
   num := 123456
   str := strconv.Itoa(num)
   fmt.Println(str)
   ```

5. **字符串转byte**

   ```go
   str := "hello"
   var bytes = []byte(str)
   fmt.Println(bytes)
   
   //byte数组转字符串
   str2 := string([]byte{'a','b','c'})
   fmt.Println(str2)
   ```

6. **10进制转2、8、16进制**

   ```go
   //strconv.FormatInt(int,int)第二个int表示转换进制数
   n := strconv.FormatInt(12,2)
   fmt.Println("12 的二进制为 ", n)
   ```

7. **查找字串是否存在**

   ```go
   //返回true/false
   flg := strings.Contains("hello","ll")
   fmt.Println(flg)
   
   //计算主串中有几个字串
   count := strings.Count("hello","l")
   fmt.Println(count)
   
   //查看主串中第一个字串的下标，没有则返回-1
   index := strings.Index("hello","llo")
   fmt.Println(index)
   
   //字串最后一次出现的下标	strings.LastIndex()
   ```

8. **字符串比较**

   ```go
   //==比较是区分大小写的，而EqualFold不区分大小写
   str1 := "abc"
   str2 := "Abc"
   fmt.Println(str1 == str2)
   fmt.Println(strings.EqualFold(str1,str2))
   ```

9. **字符串替换**

   ```go
   //最后一个参数表示替换几个  -1代表全部
   str := "hello hello world"
   str = strings.Replace(str,"hello","你好",-1)
   fmt.Println(str)
   ```

10. **字符串替换**

    ```go
    //第二个参数表示按照那个参数切割
    str := "hello hello world"
    strarray := strings.Split(str," ")
    fmt.Println(strarray)
    ```

    
