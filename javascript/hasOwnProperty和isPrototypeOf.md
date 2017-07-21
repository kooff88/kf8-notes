# js中的hasOwnProperty和isPrototypeOf方法使用实例

- hasOwnProperty: 是用来判断一个对象是否有你给出名称的属性或对象。不过需要注意的是，此方法无法检查该对象的原型链中  
  是否具有该属性，该属性必须是对象本身的一个成员.  

- isPrototypeOf:是用来判断要检查其原型链的对象是否存在于指定对象实例中，是则返回true否则返回false.   

代码
```
function siteAdmin(nickName,siteName){
  this.nikeName = nikeName;
  this.siteName = siteName;
}

siteAdmin.prototype.showAdmin = function(){
  console.log(this.nickName + '是' +this.siteName + ''的站长)
}

siteAdmin.prototype.showSite = function (){
  this.siteUrl = siteUrl;
  return this.siteName + "的地址是" + this.siteUrl;
}

var matou = new siteAdmin('你很666','WEB前端开发')
var matou2 = new siteAdmin('你很233','WEB前端开发')

matou.age = "30";
 
// matou.showAdmin();

console.log(matou.hasOwnProperty("nickName")) //true
console.log(matou.hasOwnProperty("age")); //true
console.log(matou.hasOwnProperty("showAdmin")) //false
console.log(matou.hasOwnProperty("siteUrl")); //false
console.log(matou.prototype.hasOwnProperty("showAdmin"))//true
console.log(matou.prototype.hasOwnProperty("siteUrl")); //false
console.log(matou.prototype.isPrototypeOf(matou)) //true
console.log(matou.prototype.isPrototypeOf(matou2)) //true
```
