# Node.js



Node.js是什么？？？



## Node.js简介

node.js是能够在服务器端运行JavaScript的开放源代码、跨平台JavaScript运行环境。



## Node服务器

Node处理是单线程的，但是后台拥有一个I/O线程池



## 模块化

在node中，一个js就是一个模块

在node中，每一个js模块也就是每个模块的代码都是独立运行在一个函数内的（不是全局范围，因此不能直接在其他模块直接访问）

- **引入其他模块**

    ```js
    /*
    	通过require函数引入
    	引入相对路径必须使用./或者../等开头
    	
    	require函数会返回引入模块的对象
    */
    var xxx = require("./xxx.js");
    ```

- **向外部暴露变量或方法**

    ```js
    /*
    	使用export向外部暴露
    */
    exports.x = 10
    ```

    