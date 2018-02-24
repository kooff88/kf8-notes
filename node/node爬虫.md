# Node.js 写一个普通爬虫

###  依赖

- express  
- request  
- cheerio  

### 核心代码

index.js
```js
  var express = require('express');
var app = express();
var request = require('request');
var cheerio = require('cheerio');

app.get('/', function(req,res){

  request('http://www.jd.com',function(error,response,body){
    if (!error && response.statusCode === 200){
      $ = cheerio.load(body);
      let obj = $('.cate_menu_item');

      let array = [];
      for(var i = 0; i<obj.length; i++ ){
        let strName = String(i+1);
        let namespace =  obj[i].namespace;
        array.push(namespace);
      }
      res.json({
        cat:array
      });
    }
  })
});

var server = app.listen(3000, function(){
  console.log('listening at 3000');
});

```


package.json
```json
  
  {
  "name": "pachong",
  "version": "1.0.0",
  "description": "",
  "main": "index.js",
  "scripts": {
    "start": "node index.js"
  },
  "author": "",
  "license": "ISC",
  "dependencies": {
    "cheerio": "^1.0.0-rc.2",
    "express": "^4.16.2",
    "request": "^2.83.0"
  }
}

```

### npm run start

查看localhost: 3000 
