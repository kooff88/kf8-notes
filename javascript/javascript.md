## 目录  

- [javascript合并两个json对象](#javascript合并两个json对象)
- [Promise(es6)](#Promise(es6))
- [Promise.all](#Promise.all)
- [js 小写字符串转换为大写字母](#js 小写字符串转换为大写字母)
- [获取网址中数字](#获取网址中数字)
- [函数优化](#函数优化)
- [水平滚动条](#水平滚动条)
- [new FormData()](#new FormData())
- [window.scrollTo](#window.scrollTo)
- [typeof与instanceof](#typeof与instanceof)
- [hasOwnProperty](#hasOwnProperty)
- [计算天数差](#计算天数差)
- [一个月之前日期](#一个月之前日期)
- [采用正则表达式获取地址栏参数](#采用正则表达式获取地址栏参数)
- [().toString(36)](#().toString(36))
- [获取文件类型](#获取文件类型)
- [preventDefault](#preventDefault)
- [splice](#splice)
- [event.clientX,event.clientY](#event.clientX,event.clientY)
- [获取url参数](#获取url参数)
- [arr.unshift](#arr.unshift)


## javascript合并两个json对象

```
  $.mergeJsonObject = function(jsonobject1,jsonobject2){
    var resultJsonObject = {};
    for(var attr in jsonobject1){
      resultJsonObject[attr] = jsonobject1[attr];
    }  
    for(var attr in jsonobject2){
      resultJsonObject[attr]=jsonobject2[attr];
    }

    return resultJsonObject;
  }

```

## Promise(es6)

  es6 原生提供了Promise对象

  Promise 是一个对象,用来传递异步操作的消息. 他代表了某个未来才会知道结果的事件(通常是一个异步操作),并且这个事件
  提供统一的api，可供进一步处理。

  两个特点：
  （1） 对象的状态不受外界影响。 Promise对象代表一个异步操作,三种状态：Pending,Resolved,Rejected.
       只有异步操作的结果，可以决定当前是哪一种状态，任何其他操作都无法改变这个状态.
   (2)  一旦状态改变，就不会再变，任何时候都可以得到这个结果
        状态改变:Pending->Resolved    Pending->Rejected

   ```
   example:

   var promise = new Promise(function(resolve,reject){
      if(/*异步操作成功 */){
        resolve(value);
      }else{
        reject(error);
      }
    })

    Promise 构造函数接受一个函数作为参数，该函数的两个参数分别是  resolve,reject
   异步操作成功  Pending->Resolved    
   异步操作失败  Pending->Rejec

   ```
   

## js 小写字符串转换为大写字母
  ```
   'Null'.toUpperCase()

   result: NULL

  ```


## Promise.all
-  Promise.all 是在所有的Promise对象都执行完成之后resolve.参数是一个数组  
  ，数组的每一项都是一个Promise对象就可以  

```
Promise.all([
  promise1,
  promise2
]).then(function(){
  //do something
});

Promise.all([Promise.resolve(),Promise.resolve()]).then(function(){
  //do something
})

比如你有两个异步的执行:

Promise.all([
  new Promise(function(resolve){
    setTimeout(function(){
      resolve();
    },2000)
  }),
  new Promise(function(resolve){
    setTimeout(function(){
      resolve();
    },1000)
  })
])

```

## 获取网址中数字

```
  var str=location.pathname;
  var  m=str.match(/\/aaa\/([0-9]+)/);
```

```
  react : (在框架配置好)
  this.props.match.params.id,
  
```

## 函数优化

```
  未优化
  function trim(string){
    function trimStart(string){
      return string.replace(/^s+/g,"")
    }
    function trimEnd(string){
      return string.replace(/s+$/g,"")
    }

    return trimEnd(trimStart(string))
  }

  优化
  function trimStart(string){
    return string.replace(/^s+/g,"")
  }

  function trimStart(string){
    return string.replace(/^s+/g,"")
  }

  function trim(string){
    return trimEnd(trimStart(string))
  }

```

# 水平滚动条

```
 css: 
    overflow-x:scroll
    overflow-x: auto
    overflow-y:hidden
```

# new FormData()

```
  var formdata = new FormData();
  formdata.append('name','fdipzone');
  formdata.append('gender','male');
```


# window.scrollTo


```
  function scrollWindow(){
    window.scrollTo(100,500); //滚动到指定的坐标 x=100 y=500位置
  }
```

# typeof与instanceof

```
  typeof 返回一个变量的基本类型, number,boollean,string,object,undefined,function

  alert(typeof(1));//number
  alert(typeof("abc"));//string
  alert(typeof(true));//boolean
  alert(typeof(m));//undefined


  instanceof 返回以个布尔值
  alert(a instanceof Object);  //true
  alert(b instanceof Array);  //true

  需要注意的是，instanceof只能用来判断对象和函数，不能用来判断字符串和数字等
  var b = '123';
  alert(b instanceof String);  //false
```


## hasOwnProperty
- hasOwnProperty()函数用于指示一个对象自身是否具有指定名称的属性，如果有，返回true,否则返回false  

```
object.hasOwnProperty(propertyName)
```


## 计算天数差

```
var s1 = '2012-05-12';

s1 = new Date(s1.replace(/-/g, "/"));
s2 = new Date();

var days = s2.getTime() - s1.getTime();
var time = parseInt(days / (1000 * 60 * 60 * 24));

```

## 一个月之前日期

```
let nowdate = new Date()
  nowdate.setMonth(nowdate.getMonth()-1);
```


## 采用正则表达式获取地址栏参数

```
  
function GetQueryString(name){
   var reg = new RegExp("(^|&)"+ name +"=([^&]*)(&|$)");
   var r = window.location.search.substr(1).match(reg);
   if(r!=null)return  unescape(r[2]); return null;
}
 
// 调用方法
alert(GetQueryString("参数名1"));
alert(GetQueryString("参数名2"));
alert(GetQueryString("参数名3"));
```


## ().toString(36)

toString()方法可把一个Number对象转换为一个字符串，并返回结果。

> 语法    NumberObject.toString(radix)

> radix  ： 可选。规定表示数字的基数，使2-36之间的整数。若省略该参数，则使用基数10，  
            如果该参数是10以外的其他值，则ECMAScript标准允许实现返回任意值。

().toString(36)代表36进制，其他一些也可以，比如toString(2)、toString(8)，代表输出为二进制和八进制。  
最高支持几进制，你去查下API文档就知道了。  

## 获取文件类型

- mimetype  获取文件后缀  

file.mimetype  

## preventDefault

- 取消事件的默认动作  

```
  event.preventDefault()
```

说明：   
  该方法将通知Web浏览器不要执行与事件关联的默认动作(如果存在这样的动作). 例如，如果type属性是"submit",在事件传播的任意阶段  
  可以调用人意的事件句柄，通过调用该方法，可以阻止提交表单。注意，如果Event对象的cancelable属性是false,那么久没有默认动作,  
  或者不能阻止默认动作。无论哪种情况，调用该方法都没有作用.  

## splice

- splice()方法向／从数组中添加／删除项目，然后返回被删除的项目

```
语法：
  arrayObject.splice(index,howmany,item1,......,itemX)
```

```
  参数               描述
  index             必须。整数，规定添加／删除项目的位置，使用负数可从数组结尾处规定位置。
  howmany           必须。要删除的项目数量。如果设置为0，则不会删除项目。
  item1,...,itemX   可选。向数组添加的新项目 
```

栗子：
```
  <script type="text/javascript">

var arr = new Array(6)
arr[0] = "George"
arr[1] = "John"
arr[2] = "Thomas"
arr[3] = "James"
arr[4] = "Adrew"
arr[5] = "Martin"

document.write(arr + "<br />")
arr.splice(2,0,"William")
document.write(arr + "<br />")

</script>


...

输出：

George,John,Thomas,James,Adrew,Martin
George,John,William,Thomas,James,Adrew,Martin

```

## event.clientX,event.clientY

- 事件属性   
  返回当事件被触发时鼠标指针向对于浏览器页面(客户区)的水平（垂直）坐标。  

```
  event.clientX
  event.clientY
```


## 获取url参数
```
function getUrlParam(name){
  var reg = new RegExp("(^|&)"+ name +"=([^&]*)(&|$)"); //构造一个含有目标参数的正则表达式对象
  var r = window.location.search.substr(1).match(reg);  //匹配目标参数
  if (r!=null) return unescape(r[2]); return null; //返回参数值
} 
```

## arr.unshift

```
  <script type='text/javascript'>
    var arr = new Array()
    arr[0] = "apple"
    arr[1] = "orange"
    arr[2] = "banana"

    document.write(arr+ "<br/>")
    document.write(arr.unshift("pear") + "<br/>")
    document.write(arr)   ---->>  (apple,orange,banana,pear)
  </srcipt>
```
