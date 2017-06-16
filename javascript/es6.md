# 目录

- [for-of遍历](#for-of遍历)
- [各种遍历](#各种遍历)
- [map](#map)

# for-of遍历

- for-of循环

```
  for(var value of myArray) {
    console.log(value);
  }
```

- 优点: 这是最简洁，最直接的遍历数组元素的语法
- 这个方法避开for-in 循环的所有缺陷
- 与forEach不同,它可以正确响应break,continue和return语句
- for-in循环用来遍历对象属性
- for-of 遍历 数组

- 它支持Map和 Set对象

- Set对象可以自动排除重复项:

```
  var uniqueWords = new Set(words);
```

- 生成Set对象后，你可以轻松遍历它所包含的内容:

```
  for (var word of uniqueWords) {
   console.log(word);
  }
```

- Map 对象稍有不同:内含的数据由键值对组成，所以你需要使用解构(destructuring)来将键值对拆解为两个独立的变量：

```
  for (var [key,value] of phoneBookMap){
    console.log(key + "'s phone number is: " + value)
  }

```

- 向控制台输出对象的可枚举属性

```
  for(var key of Object.keys(someObject)){
    console.log(key + ":" + someObject[key]);
  }
```

## 各种遍历

1. forEach
   forEach 是Array新方法中最基本的一个，就是遍历，循环。
   ```
   [1,2,3,4].forEach(alert);
   等同于：
   var array = [1,2,3,4];
   for (var k = 0, length = array.length; k < length; k++) {
      alert(array[k]);
   }

   Array在ES5新增的方法中，参数都是function类型，默认有传参，这些参数分别是:
   [1,2,3,4].forEach(console.log);

    // 结果：

    // 1, 0, [1, 2, 3, 4]
    // 2, 1, [1, 2, 3, 4]
    // 3, 2, [1, 2, 3, 4]
    // 4, 3, [1, 2, 3, 4]

    三个参数 : 
    [].forEach(function(value, index, array) {
      // ...
    });

    举例：
    var database = {
      users:["张含韵","江一燕","李小璐"],
      sendEmail:function(user){
        if(this.isValidUser(user)){
          console.log("你好,"+user);
        }else{
          cosnole.log("抱歉,"+user+",你不是本家人");
        }
      },
      isValidUser:function(user){
        return /^张/.test(user);
      }
    }


    //给每个人发邮件

    database.users.forEach(  //database.users中人遍历
      database.sendEmail,    //发送邮件
      database               //使用database代替上面标红的this
    );


    //结果：
    // 你好，张含韵
    // 抱歉，江一燕，你不是本家人
    // 抱歉，李小璐，你不是本家

    如果这第2个可选参数不指定，则使用全局对象代替(在浏览器是window),严格模式下甚至是undefined
    另外，forEach不会遍历纯粹"占着官位吃空饷"的元素，例如下面的例子：

    var array = [1,2,3];

    delete array [1];
    alert(array) // "1,,3"

    alert(array.length)

    alert(array.length); // but the length is still 3

    array.forEach(alert); // 弹出的仅仅是1和3
   ```

2. map  
   指"映射". [].map;基本用法跟forEach类似:  

   ```
   array.map(callback,[thisObject]);

   callback的参数也类似:

   [].map(function(){
      // ...
   })

   "映射",就是原数组被“映射”成对应新数组。下面这个例子是数值项求平方：

   var data = [1,2,3,4];

   var arrayOfSquares = data.map(function(item){
      return item * item;
   });

   console.log(arrayOfSquares); // 1,4,9,16

   var data = [1, 2, 3, 4];
   var arrayOfSquares = data.map(function() {});

   arrayOfSquares.forEach(console.log);
   结果如下图，可以看到，数组所有项都被映射成了undefined：


  var users = [
    {name : "张含韵","email":"zhang@email.com"},
    {name : "张一燕","eamil":"jiang@email.com"},
    {name : "李小璐","email":"li@email.com"}
  ];

  var emails = users.map(function(user){ return user.email });

  console.log(emails.join(",")); //zhang@email.com, jiang@email.com, li@email.com


   ```

3. filter 
  filter为"过滤"，“筛选”之意。指数组filter后，返回过滤后的新数组。用法跟map极为相似:

  array.filter(callback,[thisObject]);

  filter的callback函数需要返回布尔值true或false,如果为true组表示通过!false ,抛弃

  ```
  var data = [0, 1, 2, 3];
  var arrayFilter = data.filter(function(item) {
      return item;
  });
  console.log(arrayFilter); // [1, 2, 3]
  ```

## Map 

- 用法

```
  var map = new Map();
  map.set('name','zxguan');
  map.set('age',27);
  map.get('name');
  map.get('age');

```

- 通过 console.log(map);打印出的结果:Map {'name' => 'zxguan','age' => 27}   

- 数组作为构造参数

- Map接收一个数组作为构造函数的参数。该数组的成员是一个个表示键值对的数组.  

```
  var map = new Map([['name','zxguan'],['age','27']]);
  console.log(map);
```

- 结果一样也是 Map {'name' =>'zxguan','age' => 27}

- 以上的代码实际上等同与:

```
  var map = new Map();
  [['name','zxguan'],['age','age']].forEach(([key,value]) => map.set(key,value));

```

- 迭代
- 有以下方法来遍历一个Map:

- keys()返回所有的键名  
- values()返回所有的值  
- entries()返回所有的成员实体  
- forEach()遍历Map所有的成员  

```
  var map = new Map([['name','zxguan'],['age','27']]);

  var keys = map.keys();  //遍历key
  for(let key of keys){
    console.log(key);
  }

  var values = map.values();  //遍历Value
  for(let value of values){
     console.log(value);
  }

  var entries = map.entries();//遍历实体
  for(let [key,value] of entries){
    console.log(key,value);
  }

  map.forEach((value,index) => {
    console.log("key:"+index + "value:"+value);
  })

  var reporter = {
    report:function(key,value){
      console.log("Key: %s, Value: %s",key,value)
    }
  }

  map.forEach(function(value,key,mao){ //forEach的第二个方法用来绑定this
    this.report(key,value);

  },reporter);
```

- 常用的方法

- map.clear(): clear方法清除所有成员，没有返回值
- map.delete(key): 删除键为key的成员。删除成功，返回true;删除失败，返回false.
- map.entries();返回所有的成员实体
- forEach(calllback); 遍历map所有的成员
- get(key):读取key对应的键值，如果找不到key,返回undefined
- has(key):返回一个布尔值，表示某个键是否在map数据结构中
- keys():返回所有的键名
- set(key,value):设置key所对应的键值，然后返回整个map结构.如果key已经有值，则键值会被更新，否则就新建一个成员
- size属性：属性返回map结构的成员总数.
- values():返回所有的值

- 值得注意的是,只有对同一个对象的引用，map才会视为同一个key.如：

```
var map = new Map();
map.set(['KEY'],5);
var value = map.get(['KEY']);
console.log(value); //undefined

var key1 = ['KEY'];
var key2 = ['KEY'];
var map = new Map();
map.set(key1,'AAA');
map.set(key2,'BBB');
console.log(map.get(key1)); //AAA
console.log(map.get(key2)); //BBB

```

- 如果要将Map转换为数组，可以使用扩展运算符 (...)

```
  var  myMap = new Map().set(true,7).set({foo:3},['abc']);
  console.log([...myMap]);
```

- 以下是一些常用的转换工具方法:

```
//Map 转Object对象
function map2Obj(map){
  let obj = {};
  for (let [key,value] of map){
    obj[key] = value;
  }
  return obj;
}

// Object对象转Map
function obj2Map(obj){
  let map = new Map();
  for (let key of Object.keys(obj)){
    map.set(key,obj[key]);
  }
  return map
}

// Map转为Json
function map2Json(map){
 let keys = map.keys();
 let isAllKeyStr = true; //是否key全部为字符串
 for(let key of keys){
  if (!((typeof key == 'string')&& (key.constructor == String))){
    isAllKeyStr == false;
    break;
  }
 }
 if(isAllKeyStr){
  return JSON.stringify(map2Obj(map));
 }else{
  reutrn JSON.stringify([...map]);
 }
}

JSON转为Map
function json2Map(json){
  let _json = JSON.parse(json);
  if(Array.isArray(_json)){
    return new Map(JSON.parse(json));    
  }else{
    return obj2Map(JSON.parse(json));
  }
}
```



