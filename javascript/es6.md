# 目录

- [遍历](#遍历)

# 遍历

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



