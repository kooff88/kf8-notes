### 目录

- [webpack](#webpack)

# webpack

- 一个常见的Webpack配置文件  

```
  var webpack = require('webpack');
  var HtmlWebpackPlugin = require('html-webpack-plugin');
  var ExtractTextPlugin = require('extract-text-webpack-plugin');

  module.exports = {
    devtool:'eval-source-map', //配置生产Source Maps,选择合适的选择
    entry:__dirname + "/app/main.js",
    output:{
      path: __dirname + "/build",
      filename:"[name]-[hash].js"
    },

    module:{
      loaders: [
        {
          test:/\.json$/,
          loader:'json'
        },
        {
          test:/\.js$/,
          exclude:/node_modules/,
          loader:'babel',
          query:{
            presets:['es2015',react] //允许使用es6以及JSX语法 
          }
        },
        {
          test:/\.css$/,
          loader:ExtractTextPlugin.extract('style','css?module!postcss')
        }
      ]
    },
    postcss:[ // css预处理器
      require('autoprefixer') //调用autoprefixer插件
    ],

    plugins:[
      new HtmlWebapkPlugin({
        template: __dirname + "/app/index.tmpl.html"
      }),
      new webpack.optimize.OccurenceOrderPlugin(),
      new webpack.optimize.UglifyJsPlugin(),
      new ExtractTextPlugin("[name]-[hash].css")
    ],
    devServer:{
      contentBase:"./public", //本地服务器所加载的页面所在目录
      colors:true, //终端中输出结果为彩色
      historyApiFallback:true, //不跳转
      inline:true //实时刷新
    }
  }
```

# Loaders 
- :使用不同的 loader,webpack通过调用外部的脚本或工具可以对 各种各样的格式的文件进行处理  


```
  //config.json (创建带问候信息的json文件)
  {
    "greetText":"hi there and greeting from JSON"
  }
```

```
  var config = require('./config.json');

  module.exports = function(){
    var greet = document.createElement('div');
    greet.textContext = config.greetText;
    return greet;
  }
```

```
  //index.html

<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8">
    <title>Webpack Sample Project</title>
  </head>
  <body>
    <div id='root'>
    </div>
    <script src="bundle.js"></script>
  </body>
</html>
```

# Bable 
- 其实是一个编译JavaScript的平台 , 几个模块化的包  

```
  //.babelsrc
  {
    "presets":["react","es2015"]
  }
```

# 一切皆模块：  
- Webpack把所有的文件都可以当作模块处理,包括你的JavaScript代码,也包括CSS和fonts以及图片等等,  
  只有通过合适的loaders,他们都可以被当作模块处理  

# css
- webpack提供两个工具处理样式表,css-loader和style-loader,二者处理的任务不同，css-loader使你  
  能够使用类似@import和url(...)的方法实现 require()的功能,style-loader将所有的计算后的样式  
  加入页面中，二者组合在一起使你能够把样式表嵌入webpack打包后的JS文件中  
 
# 插件 - Plugins
- 用来拓展Webpack功能的,它们会在整个构建过程中生效,执行相关任务  
  Loaders :是在打包构建过程中用来处理源文件(JSX,Scss,Less...),一次处理一个  
  Plugins并不直接操作单个文件，它直接对整个构建过程起作用.  

```
  ...
  plugins:[
    new webpack.BannerPlugin("Copyright Flying Unicorns inc.")
  ]
  ...
```

- HtmlWebpackPlugin  
  这个插件依据一个简单的模版m,最终生成Html5文件,这个文件中自动引用了你的大包后的js文件,  
  每次编辑都在文件名中插入一个不同的哈希值  
