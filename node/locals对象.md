# locals

- locals是Express应用中Application(app)对象和Reasponse(res)对象中的属性，该属性是一个对象。  
  该对象的主要作用是，将值传递到所渲染的模版中  

1. locals对象  
   locals对象用于将数据传递至所渲染的模版中。  
   对于如下一个ejs模版：  
   ```
    <!DOCTYPE html>
    <html>
      <head>
        <title><%= name %></title>
      </head>
      <body>
        <h1><a href="<%= url %>"><%= name %></a></h1>
        <p><%= introduce %></p>
      </body>
    </html>
   ```

我们可以像下面这样渲染页面，并向页面传递name,url,introduce三个变量的值：  

```
  router.get('/',function(req,res){
    res.render('index',{name:'IT笔记',url:'http://itbilu.com', introduce:'学习、记录、整理'})
    //也可以使用res.locals 变量
     <!-- res.locals = {
        name:'IT笔记'
          url:'http://itbilu.com', 
          introduce:'学习、记录、整理'
      } 
      res.render('index');
     -->
  })
```

渲染后的页面HTML:  

```
<!DOCTYPE html>
<html>
  <head>
    <title><IT笔录></title>
  </head>
  <body>
    <h1><a href="http://itbilu.com">IT笔录</a></h1>
    <p>学习、记录、整理</p>
  </body>
</html>
```

locals对象会被传递到页面，在模版中可以直接引用该对象的属性，也可以通过该对象引用。如：<%= name %>属性同样可以通过<%= locals.name %>来引用。  

- app.locals与res.locals  

locals可能存在于app对象中即：app.locals;也可能存在于res对象中,即：res.locals。两者都会将该对象传递至所渲染的页面中。不同的是，  
app.locals会在整个生命周期中起作用；而res.locals只会有当前请求中起作用。  
由于app.locals在当前应用所有的渲染模版中访问，这样我们就可以在该对象中定义一些顶级／全局的数据，并在渲染模版中使用  

2. 在中间件中使用  

我们常利用Exress的中间件将复杂的问题拆解成多个简单的问题，实现复杂的问题简单化。locals对象中也可以应用中间件或路由中间件中，  
该对象和app,req,res一样可以依次传递，添加或修改其属性值后，会在后面的处理中体现出来  

如，在app中使用locals:  

```
var app = express();
app.locals.name = '这是一个app'; //定义可以应用整个生命周期中使用的变量
app.use(function(req,res,next){
  app.locals.name = '新名字';//修改
  res.locals.url= 'http://itbilu.com';
  next(err);
})
```

在路由中间件中使用locals:  

```
  router.get('/',urlAndIntroduce,function(req,res){
    res.render('index',{name:'IT笔录'});
  })

  function urlAndIntroduce(req,rex,next){
    res.locals = { url:'http://itbilu.com', introduce:'学习、记录、整理'}
  }
```


