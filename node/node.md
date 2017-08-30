# js 目录 

-[Math...熟悉用法](#Math...熟悉用法)
-[npm run dev](#npm run dev)
-[markdown一些规则](#markdown一些规则)
-[删除数组中字段](#删除数组中字段)
-[moment时间处理js包](#moment时间处理js包)
-[req获取前台传来数据的集中方式](#req获取前台传来数据的集中方式)
-[fs.readdirSync](#fs.readdirSync)
-[createServer](#createServer)

## Math...熟悉用法
> Math.trunc()
    ```   
        Math.trunc(13.37);    // 13
        Math.trunc(42.84);    // 42
        Math.trunc(0.123);    //  0
        Math.trunc(-0.123);   // -0
        Math.trunc('-1.123'); // -1
        Math.trunc(NaN);      // NaN
        Math.trunc('foo');    // NaN
        Math.trunc();         // NaN
    ```

>Math.floor()
    ```   
        Math.floor( 45.95); //  45
        Math.floor( 45.05); //  45
        Math.floor(  4   ); //   4
        Math.floor(-45.05); // -46 
        Math.floor(-45.95); // -46
    ```

>Math.ceil()
    ```   
        Math.ceil(.95);    // 1
        Math.ceil(4);      // 4
        Math.ceil(7.004);  // 8
        Math.ceil(-0.95);  // -0
        Math.ceil(-4);     // -4
        Math.ceil(-7.004); // -7
    ```

>Math.round()   
    ```   
        Math.round( 20.49); //  20
        Math.round( 20.5);  //  21
        Math.round( 42  );  //  42
        Math.round(-20.5);  // -20
        Math.round(-20.51); // -21
    ```

## npm run dev

     npm run dev  dev是自定义的启动单词 
    ```
    "scripts": {
        "dev": "node build/dev-server.js",
        "build": "node build/build.js",
        "unit": "karma start test/unit/karma.conf.js --single-run",
        "e2e": "node test/e2e/runner.js",
        "test": "npm run unit && npm run e2e",
        "lint": "eslint --ext .js,.vue src test/unit/specs test/e2e/specs"
      },
    ```

## markdown一些规则  

    aaa.md 文档中 
    <> 表示必传参数  [] 表示选传参数  # 表示目录  
    详情查看网站： [http://www.appinn.com/markdown](http://www.appinn.com/markdown/)
   

## 删除数组中字段
    
    ```
    delete userd['password']  删除userd数组中 password
    ```
   
## moment时间处理js包
    
    加载：sudo npm install moment
    ```
    var moment =require('moment');
    if(TIME) TIME = moment(TIME).format("YYYY-MM-DD HH:mm:ss");修改时间格式
    或者
    if(TIME) TIME = moment(TIME,"YYYY-MM-DD HH:mm:ss");修改时间格式
    ```

## req获取前台传来数据的集中方式

    ```
    req.param 获取pathinfo中参数 /api/users/{id}
    req.query 获取查询参数 /api/users?name=wwx
    req.body  获取form提交参数
    ```

## fs.readdirSync

同步版本的 fs.readdirSync()  

方法将返回一个包含"指定目录下所有文件名称"的数组对象。  

## createServer

方法说明:  
改函数用来创建一个HTTP服务器，并将 requestListener 作为request时间的监听函数.  

```
    http.createServer([requestListener])
```

由于改方法属于http模块，使用前需要引入http模块(var http = require('http'))  

接受参数：  

requestListener 请求处理函数，自动添加到request事件，函数传递两个参数:  
    
   req 请求对象，想知道req有哪些属性,可以产看"http.request属性整合"。  

   res 相应对象, 收到请求后摇作出的响应. 想知道res有哪些属性，可以查看"http.response属性整合".  

最后调用listen函数，监听3000端口.  

```
    var http =require('http')
    http.createServer(function(req,res){
        res.writeHead(200,{'Content-type' : 'text/html'});
        res.write('<h1>Node.js</h1>');
        res.end('<h1>Hello World</h1>')
    }).listen(3000);
```



