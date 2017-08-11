# Function.apply

Function.apply(obj,args)方法能接受两个参数  
> obj:  这个对象将代替Function类里this对象  
> args: 这个是数组，它将作为参数传给Function(args --> arguments)  

栗子：  

```
function Person(name,age){ //定义一个类，人类
  this.name = name; //名字
  this.age = age; //年龄
  this.sayhello = function(){console.log('hello')};
}

function Print(){ //显示类的属性
  this.funcName = "Print";
  this.show = function(){
    var msg = [];
    for (var key in this){
      if(typeof[this[key] !=="function"]){
        msg.push([key,":",this[key].join(""));
      }
    }
    console.log(msg.join(" "))
  }
} 

function Student(name,age,grade,school){ //学生类
  Person.apply(this,arguments);
  Print.apply(this.arguments);
  this.grade = grade;
  this.school = school;
}

var p1 = new Person("jake",10)
p1.sayhello();
var s1 = new Student("tom",12,6,"清华小学")
s1.show();
s1.sayhello();
console.log(s1.funcName);
```

学生类本来不具备任何方法，但是在Person.apply(this.arguments)后，他就具备了Person类的sayhello方法和所有属性。  


#### 利用Apply的参数数组化来提高

Function.apply()在提升程序性能方面的技巧  

我们先从Math.max()函数说起，Math.max后面可以接受任意个参数，最后返回参数重最大值.  
比如:  
> console.log(Math.max(5,6,3)) // 6  


但是在很多情况下，我们需要找出数组中最大的元素。  

```
 var arr = [5,7,9,1]
 console.log(Math.max(arr)) // 这样写不行，一定要这样写  
 function getMax(arr) {
  var arrLen = arr.length;
  for(var i=0;ret=arr[0];i<arrLen;i++){
    ret = Math.max(ret,arr[i]);
  }
  return ret;
 }
```

上面方法低效  

用apply  

```
function.getMax2(arr){
  return Math.max.apply(null,arr);
}
```

这就很简洁了。