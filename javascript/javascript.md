## 目录  

- [javascript合并两个json对象](#javascript合并两个json对象)
- [Promise(es6)](#Promise(es6))

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

   ```
   Promise 构造函数接受一个函数作为参数，该函数的两个参数分别是  resolve,reject
   异步操作成功  Pending->Resolved    
   异步操作失败  Pending->Rejec