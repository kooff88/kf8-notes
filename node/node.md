# js 目录 

-[Math...熟悉用法](#Math...熟悉用法)
-[npm run dev](#npm run dev)
-[markdown一些规则](#markdown一些规则)
-[删除数组中字段](#删除数组中字段)
-[moment时间处理js包](#moment时间处理js包)
-[req获取前台传来数据的集中方式](#req获取前台传来数据的集中方式)

# Math...熟悉用法
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

# npm run dev

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

# markdown一些规则  

    aaa.md 文档中 
    <> 表示必传参数  [] 表示选传参数  # 表示目录  
    详情查看网站： [http://www.appinn.com/markdown](http://www.appinn.com/markdown/)
   

# 删除数组中字段
    
    ```
    delete userd['password']  删除userd数组中 password
    ```
   
# moment时间处理js包
    
    加载：sudo npm install moment
    ```
    var moment =require('moment');
    if(TIME) TIME = moment(TIME).format("YYYY-MM-DD HH:mm:ss");修改时间格式
    或者
    if(TIME) TIME = moment(TIME,"YYYY-MM-DD HH:mm:ss");修改时间格式
    ```

# req获取前台传来数据的集中方式

    ```
    req.param 获取pathinfo中参数 /api/users/{id}
    req.query 获取查询参数 /api/users?name=wwx
    req.body  获取form提交参数
    ```
