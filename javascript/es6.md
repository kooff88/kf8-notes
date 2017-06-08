# 目录

- [for-of遍历](#for-of遍历)
- [各种遍历](#各种遍历)

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

