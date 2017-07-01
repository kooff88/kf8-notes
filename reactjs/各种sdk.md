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
- [react-cropper](#react-cropper)
- [loading-cli](#loading-cli)
- [bodyParser](#bodyParser)
- [cross-evn安装&使用](#cross-evn安装&使用)
- [jsonwebtoken](#jsonwebtoken)
- [req.session.regenerate](#reqreq.session.regenerate)
- [classnames](#classnames)

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

# react-cropper
- 图片修剪

```
  import React, {Component} from 'react';
  import Cropper from 'react-cropper';
  import 'cropperjs/dist/cropper.css'; // see installation section above for versions of NPM older than 3.0.0
  // If you choose not to use import, you need to assign Cropper to default
  // var Cropper = require('react-cropper').default

  class Demo extends Component {
    _crop(){
      // image in dataUrl
      console.log(this.refs.cropper.getCroppedCanvas().toDataURL());
    }

    render() {
      return (
        <Cropper
          ref='cropper'
          src='http://fengyuanchen.github.io/cropper/img/picture.jpg'
          style={{height: 400, width: '100%'}}
          // Cropper.js options
          aspectRatio={16 / 9}
          guides={false}
          crop={this._crop.bind(this)} />
      );
    }
  }
```

# loading-cli
- 加载中动画

```
  var loading =  require('loading-cli');
  var load = loading("loading text!!")
   
  load.start()
   
  setTimeout(function(){
      load.color = 'yellow';
      load.text = ' Loading rainbows';
  },2000)
   
  // stop 
  setTimeout(function(){
      load.stop()
  },3000)
```


# bodyParser

```
- bodyParser.json(options)
  options可选 ， 这个方法返回一个仅仅用来解析json格式的中间件。这个中间件能接受任何body中任何Unicode编码的字符。支持自动的解析gzip和 zlib
- bodyParser.urlencoded(options)
  options可选，这个方法也返回一个中间件，这个中间件用来解析body中的urlencoded字符， 只支持utf-8的编码的字符。同样也支持自动的解析gzip和 zlib。
```


# cross-evn安装&使用

- 这个迷你的包能够提供一个设置环境变量的scripts，让你能够以unix方式设置环境变量，然后在windows上也能兼容运行。   
  在NODE_ENV=xxxxxxx前面添加cross-env就可以了。   

  ```例子
  "scripts": {
    "development": "cross-env NODE_ENV=development node ./bin/aaa",
  },
  ```

# jsonwebtoken

```
  var JWT = require('jsonwebtoken');

  exports.generateToken = function(key){
    var payload = key || Date.now();
    return JWT.sign(payload,Date.now() + "")
  }

  var aa = this.generateToken()
  console.log('aa',aa)
```

# req.session.regenerate

```
  req.session.regenerate(function(){ 
      req.session.captcha = captcha.text;
      req.session.save();                      //保存一下修改后的Session
      req.set('Content-Type','image/svg+xml'); //在html中动态插入 svg +xml格式文件
      res.status(200).send(captcha.text);      //何种状态下发送什么信息
  })
```


#classnames
- className 处理工具  

```
/* components/submit-button.js */
import { Component } from 'react';
import classNames from 'classnames/bind';
import styles from './submit-button.css';
 
let cx = classNames.bind(styles);
 
export default class SubmitButton extends Component {
  render () {
    let text = this.props.store.submissionInProgress ? 'Processing...' : 'Submit';
    let className = cx({
      base: true,
      inProgress: this.props.store.submissionInProgress,
      error: this.props.store.errorOccurred,
      disabled: this.props.form.valid,
    });
    return <button className={className}>{text}</button>;
  }
};
```
