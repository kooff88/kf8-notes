# 目录

- [Object.assign](#Object.assign)
- [Object.keys](#Object.keys)

## Object.assign


- 此方法用于将所有可枚举的属性的值从一个或多个源对象复制到目标对象。它将返回目标对象。  

##### 语法

```
  Object.assign(target, ...source)
```

参数： target 目标对象    sources(多个)源对象  

- 如果目标对象中的属性具有相同的键，则属性将被源中的属性覆盖。后来的源的属性将类似地覆盖早先的属性。  

Object.assign方法只会拷贝源对象自身的并且可枚举的属性到目标对象身上。该方法使用源对象[[Get]]和目标对象[[Set]],所以它会调用相关  
getter和setter.因此，它分配属性而不是复制或定义新的属性。如果合并源包含了getter,那么该方法就不适合将新属性合并到原型里。  
假如是拷贝属性定义到原型里，包括他们的可枚举性，那么应该使用   
Object.getOwnPropertyDescriptor() 和 Object.defineProperty() 。  

string类型和Symbol类型的属性都会被拷贝。  

ps: 在属性拷贝过程中可能会产生异常，比如目标对象的某个属性和源对象的某个属性同名，这时该方法会抛出一个TypeError异常，拷贝过程中断，  
已经拷贝成功的属性不会受到影响，还没被拷贝的属性将不会再被拷贝。  

ps: Object.assign会跳哟那些值为null或 undefined的源对象.  

####栗子：  
 
```
  var obj = { a:1 }
  var copy = Object.assign({},obj);
  console.log(copy); //{a:1}
```


- 深度拷贝问题  

 针对深度拷贝，需要其他方法，因为Object.assign()拷贝的是属性值。假如源对象的属性值时一个指向对象的引用，它也只拷贝那个应用值  

```
function test() {
  let a = { b: {c:4} , d: { e: {f:1}} }
  let g = Object.assign({},a)
  let h = JSON.parse(JSON.stringify(a));
  console.log(g.d) // { e: { f: 1 } }
  g.d.e = 32
  console.log('g.d.e set to 32.') // g.d.e set to 32.
  console.log(g) // { b: { c: 4 }, d: { e: 32 } }
  console.log(a) // { b: { c: 4 }, d: { e: 32 } }
  console.log(h) // { b: { c: 4 }, d: { e: { f: 1 } } }
  h.d.e = 54
  console.log('h.d.e set to 54.') // h.d.e set to 54.
  console.log(g) // { b: { c: 4 }, d: { e: 32 } }
  console.log(a) // { b: { c: 4 }, d: { e: 32 } }
  console.log(h) // { b: { c: 4 }, d: { e: 54 } }
}
test();
```

- 合并objects  

```
var o1 = {a:1};
var o2 = {b:2};
var o3 = {c:3};

var obj = Object.assign(o1,o2,o3);
console.log(obj); //{a:1,b:2,c:3}
console.log(o1);  // { a: 1, b: 2, c: 3 }, 注意目标对象自身也会改变。
```

拷贝symbol类型的属性  

```
  var o1 = { a:1 };
  var o2 = { [Symbol("foo"):2] };

  var obj = Object.assign({}, o1, o2);
  console.log(obj); // { a: 1, [Symbol("foo")]: 2 }
```

ps : Symbol 是一种特殊的，不可变的数据类型，可以作为对象属性的标识符使用。Symbol对象是一个symbol primitive data type的  
隐式对象包装器。  
symbol数据类型是一个primitive data type.

> var sym0 = Symbol();  
  var sym1 = Symbol("symbol1");  
  var sym2 = Symbol("symbol2");  
  var sym3 = Symbol("symbol2");  

上面的代码创建三个新的symbols.注意,Symbol('symbol2')不会强制字符串"symbol2"成为一个symbol.它每次都会创建一个新的symbol:  

> Symbol("symbol2") === Symbol("symbol2"); //false  

下面使用new 运算符的语法将会抛出一个TypeError错误：  

> var sym = new Symbol(); // TypeError  

这会阻止创建一个显式的 Symbol 包装器对象而不是一个 Symbol 值。围绕原始数据类型创建一个显式包装器对象从 ECMAScript 6  
开始不再被支持。 然而，现有的原始包装器对象，如 new Boolean、 new String以及new Number因为遗留原因仍可被创建   
如果你真地想创建一个 Symbol 包装对象(Symbol wrapper object)，你可以使用 Object() 函数  

> var sym = Symbol("foo");  
typeof sym;     // "symbol"  
var symObj = Object(sym);  
typeof symObj;  // "object"  

#### 继承属性和不可枚举属性是不能拷贝的

```
var obj = Object.create({foo: 1}, { // foo 是个继承属性。
    bar: {
        value: 2  // bar 是个不可枚举属性。
    },
    baz: {
        value: 3,
        enumerable: true  // baz 是个自身可枚举属性。
    }
});

var copy = Object.assign({}, obj);
console.log(copy); // { baz: 3 }
```

## Object.keys

在实际开发中，我们有时需要知道对象的所有属性，原生js给我们提供了很好的方法 : Object.keys(),该方法返回一个数组  

传入对象，返回属性名:  

```
var obj = { 'a':'123','b':'345' };
console.log(Object.keys(obj)) ; // ['a','b']

var obj1 = { 100:"a",2:"b",7:"c" }
console.log(Object.keys(obj)); //["2","7","100"]

var obj2 = Object.create({},{ getFoo:{value : function(){ return this.foo }} });
obj2.foo = 1; 
console.log(Object.keys(obj2)); // ["foo"]
```

传入字符串，返回索引  

```
  var str = 'ab1234';
  console.log(Object.keys(obj)); // [0,1,2,3,4,5]
```

构造函数 返回空数组或者属性名

```
  function Pasta(name,age,gender){
    this.name = name;
    this.age = age;
    this.gender =gender;
    this.toString = function(){
      return (this.name + ", " + this.age + ", " + this.gender);
    }
  }

  console.log(Object.keys(Pasta)); //console: []

  var spaghtti = new Pasta("Tom",20,"male")
  console.log(Object.keys(spaghetti)); //console: ["name","age","gender","toString"]
```

数组返回索引  

```
  var arr = ["a","b","c"];
  console.log(Object.keys(arr)); // console: ["0","1","2"]
```
