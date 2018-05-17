# serve-favicon

有一个名称为 serve-favicon的中间件，可以用于请求网页的logo。

使用方法：  

```js

	var connect = require('C:/Users/node_modules/connect'); // connect 中间件的路径
	var http = require('http');
	var favicon =require('C:/Users/node_modules/serve-favicon'); // serve-favicon 中间件的路径

	// __dirname 代表该执行文件的父目录，注意是双下划线，
	var app = connect()
				.use(favicon(__dirname + '/public/favicon.ico')) 
				.use(function(req,res){
					res.end('hello world')
				})

  http.createServer(app).listen(9527);

```

将favicon.ico 图标放在pulic文件下面