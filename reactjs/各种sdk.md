# 目录 各种sdk

- [dotenv](#dotenv)
- [chalk](#chalk)
- [connect-history-api-fallback](#connect-history-api-fallback)
- [http-proxy-middleware](#http-proxy-middleware)
- [detect-port](#detect-port)
- [react-dev-utils](#react-dev-utils)
- [extract-text-webpack-plugin](#extract-text-webpack-plugin)
- [promise](#promise)
- [object-assign](#object-assign)

# dotenv

- 加载环境变量  
```
npm install dotenv --save

DB_HOST=localhost
DB_USER=root
DB_PASS=s1mpl3

...

var db = require('db')
db.connect({
  host: process.env.DB_HOST,
  username: process.env.DB_USER,
  password: process.env.DB_PASS
})
```

## chalk

- 样式处理sdk

```
$ npm install --save chalk

console.log(chalk.blue('Hello world!'));
console.log(chalk.blue('Hello') + 'World' + chalk.red('!'));

console.log(chalk.blue.bgRed.bold('Hello world!'));

console.log(chalk.blue('Hello', 'World!', 'Foo', 'bar', 'biz', 'baz'));

console.log(chalk.red('Hello', chalk.underline.bgBlue('world') + '!'));

console.log(chalk.green(
  'I am a green line ' +
  chalk.blue.underline.bold('with a blue substring') +
  ' that becomes green again!'
));

console.log(`
CPU: ${chalk.red('90%')}
RAM: ${chalk.green('40%')}
DISK: ${chalk.yellow('70%')}
`);

const chalk = require('chalk');
const error = chalk.bold.red;
console.log(error('Error!'));
```

## connect-history-api-fallback
- 单页面路由处理更自然

```
npm install --save connect-history-api-fallback


var history = require('connect-history-api-fallback');


var connect = require('connect');
var app = connect()
  .use(history())
  .listen(3000);



var express = require('express');
var app = express();
app.use(history());
```

## http-proxy-middleware

- http-proxy-middleware 是一套 Node.js 代理中间件 for connect, express 和 browser-sync。

```
var proxy = require('http-proxy-middleware');
 
var apiProxy = proxy('/api', {target: 'http://www.example.org'});

var apiProxy = proxy('http://www.example.org/api');

```

## detect-port

- 测试端口是否被占用  

```
  $ npm i detect-port --save
  const detect = require('detect-port');

  detect(port, (err, _port) => {
    if (err) {
      console.log(err);
    }
   
    if (port == _port) {
      console.log(`port: ${port} was not occupied`);
    } else {
      console.log(`port: ${port} was occupied, try port: ${_port}`);
    }
  });
```

## react-dev-utils

- webpack2插件 ,清理屏幕  

```
   var clearConsole = require('react-dev-utils/clearConsole');
   clearConsole();
   console.log('Just cleared the screen!');
```

```
  var path = require('path');
  var checkRequiredFiles = require('react-dev-utils/checkRequiredFiles');

  if (!checkRequiredFiles([
    path.resolve('public/index.html'),
    path.resolve('src/index.js')
  ])) {
    process.exit(1);
  }
```

```
var webpack = require('webpack');
var config = require('../config/webpack.config.dev');
var formatWebpackMessages = require('react-dev-utils/formatWebpackMessages');
 
var compiler = webpack(config);
 
compiler.plugin('invalid', function() {
  console.log('Compiling...');
});
 
compiler.plugin('done', function(stats) {
  var rawMessages = stats.toJson({}, true);
  var messages = formatWebpackMessages(rawMessages);
  if (!messages.errors.length && !messages.warnings.length) {
    console.log('Compiled successfully!');
  }
  if (messages.errors.length) {
    console.log('Failed to compile.');
    messages.errors.forEach(e => console.log(e));
    return;
  }
  if (messages.warnings.length) {
    console.log('Compiled with warnings.');
    messages.warnings.forEach(w => console.log(w));
  }
});  

```

```
var getProcessForPort = require('react-dev-utils/getProcessForPort');
 
getProcessForPort(3000);

```

```
var path = require('path');
var openBrowser = require('react-dev-utils/openBrowser');

if (openBrowser('http://localhost:3000')) {
  console.log('The browser tab has been opened!');
}
```

```
var path = require('path');
var WatchMissingNodeModulesPlugin = require('react-dev-utils/WatchMissingNodeModulesPlugin');

// Webpack config
module.exports = {
  // ...
  plugins: [
    // ...
    // If you require a missing module and then `npm install` it, you still have
    // to restart the development server for Webpack to discover it. This plugin
    // makes the discovery automatic so you don't have to restart.
    // See https://github.com/facebookincubator/create-react-app/issues/186
    new WatchMissingNodeModulesPlugin(path.resolve('node_modules'))
  ],
  // ...
}
```

```
var path = require('path');
var HtmlWebpackPlugin = require('html-dev-plugin');
var InterpolateHtmlPlugin = require('react-dev-utils/InterpolateHtmlPlugin');

// Webpack config
var publicUrl = '/my-custom-url';

module.exports = {
  output: {
    // ...
    publicPath: publicUrl + '/' 
  },
  // ...
  plugins: [
    // Makes the public URL available as %PUBLIC_URL% in index.html, e.g.:
    // <link rel="shortcut icon" href="%PUBLIC_URL%/favicon.ico">
    new InterpolateHtmlPlugin({
      PUBLIC_URL: publicUrl
      // You can pass any key-value pairs, this was just an example.
      // WHATEVER: 42 will replace %WHATEVER% with 42 in index.html.
    }),
    // Generates an `index.html` file with the <script> injected.
    new HtmlWebpackPlugin({
      inject: true,
      template: path.resolve('public/index.html'),
    }),
    // ...
  ],
  // ...
}
```



##extract-text-webpack-plugin

```
const ExtractTextPlugin = require('extract-text-webpack-plugin');
 
module.exports = {
  module: {
    rules: [
      {
        test: /\.scss$/,
        use: ExtractTextPlugin.extract({
          fallback: 'style-loader',
          //resolve-url-loader may be chained before sass-loader if necessary 
          use: ['css-loader', 'sass-loader']
        })
      }
    ]
  },
  plugins: [
    new ExtractTextPlugin('style.css')
    //if you want to pass in options, you can do so: 
    //new ExtractTextPlugin({ 
    //  filename: 'style.css' 
    //}) 
  ]
}
```

## promise

- $ npm install promise

```
var Promise = require('promise');
 
var promise = new Promise(function (resolve, reject) {
  get('http://www.google.com', function (err, res) {
    if (err) reject(err);
    else resolve(res);
  });
});

```

```
var Promise = require('promise/setimmediate');
```

```
var Promise = require('promise/lib/es6-extensions');
```



## object-assign

```
$ npm install --save object-assign


const objectAssign = require('object-assign');
 
objectAssign({foo: 0}, {bar: 1});
//=> {foo: 0, bar: 1} 
 
// multiple sources 
objectAssign({foo: 0}, {bar: 1}, {baz: 2});
//=> {foo: 0, bar: 1, baz: 2} 
 
// overwrites equal keys 
objectAssign({foo: 0}, {foo: 1}, {foo: 2});
//=> {foo: 2} 
 
// ignores null and undefined sources 
objectAssign({foo: 0}, null, {bar: 1}, undefined);
//=> {foo: 0, bar: 1} 
```
