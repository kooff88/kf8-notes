# 目录

[sequelize基本用法](#sequelize基本用法)
[sequelize.and||sequelize.or](#sequelize.and||sequelize.or)
[sequelize.query用法](#sequelize.query用法)
[sequelize.findOrCreate](#sequelize.findOrCreate)
[logging 使用](#logging 使用)
[sequelize.bulkCreate](#sequelize.bulkCreate)
[sequelize建表](#sequelize建表)
[setDataValue,getDataValue](#setDataValue,getDataValue)

# sequelize基本用法

1.加载:

   ```
   npm install sequelize
   ```

2.引用

  ```
  var Models = require('../model');
  ```

3.使用

     
  ```
  **建表**
  module.exports = function(sequelize,DataTypes){
    sequelize.define("people",{
      name:DataTypes.STRING(220),
      age :DataTypes.INTEGER(11),
      bornTime: DataTypes.DATE,
      ...
   };
   return people;
  }
   

   **拉取列表**

   perpage = parseInt(perpage);
    page = parseInt(page);
    
    Models.exhibition.findAndCountAll({
      where :{
        deleted:0 
      },
      'offset': perpage * (page - 1), // 跳过多少条
      'limit': perpage  
    }).then(function(results){
      if(!results) return res.json({ "code":1003,"message":"获取列表失败"})
      var page_count = Math.ceil(results.count/perpage);
      var results = {
        "total" : results.count,
        "data"  :  results.rows,
        "page"  :  page,
        "page_count": page_count,
      }
      res.json({
        "code":0,
        "message":"获取列表成功！",
        "results":results
      })
    }).catch(function(err){
      console.log("--Appointment_list  ->err",err)
      return res.json({"code":100404, "message":err.message});
    });




    **添加**

    Models.appointment.create({
      "name":"小张",
      "age":"30"
    }).then (function(results){
      if(!results) return res.json({"code":1003, "message":"添加预约失败!"})
      res.json({
        "code":0,
        "message":" 添加成功",
        "results":results.dataValues
      })  
    }).catch(function(err){
      console.log("--create appointment  ->err",err);
      return res.json({"code":10040, "message":err.message})
    })



    **获取单条**

    Models.appointment.findOne({
      'where': {'id':sid}
    }).then(function(results){
      if(!results) return res.json({"code" : 1003 , "message" : "获取预约失败!"});
      var results = results.dataValues ;
      res.json({
        "code" : 0,
        "message" : "获取预约信息成功",
        "data" : results
      })
    }).catch(function(err){
      console.log("--find appointment getInfo ->err",err);
      return res.json({"code":10040,"message":err.message})
    })



     **删除**
     Models.appointment.destory({
        where:{
          "id" : sid
        }
      }).then(function(results){
        if(!results) return res.json({"code":1003,"message":"删除预约失败!"})
        res.json({
          "code":0,
          "message":"删除预约成功!"
        }) 
      }).catch(function(err){
        console.log("--delete appointent -->err",err);
        return res.json({"code":10040,"message":err.message})
      })  



      **更新** 
      Models.appointment.update({
        "name":"小张",
        "age":"30"
      } ,{
          where : { "id" :sid }
      }).then(function(results){
        if(!results) return res.json({"code":1003,"message":"更新失败!" })
          res.json({
          "code": 0,
          "message" :"更新成功!"
        }) 
      }).catch(function(err){
        console.log("--update appointment ->err",err);
        return res.json({"code":10040,"message":err.message})
      })
  ```


# sequelize.and||sequelize.or
   
  ```
   where : Sequelize.and(
     { deleted:0 },
     Sequelize.or(
     {title : { like: keyword + '%' } }
  )

  ```

# sequelize.query用法

  ```
    Models.sequelize.query(sql,{type:Sequelize.QueryTypes.SELECT}).then(function(result){     

    }).catch(...)

  ```
  上段代码中的 {type:Sequelize.QueryTypes.SELECT} 一定要加上 不让结果不准确


# sequelize.findOrCreate

## logging 使用
-  官方文档：

  [options.logging = console.log]   Boolean|function 

  A function that logs sql queries,or false for no logging

  
  ```
  for example:

  [function]
  var self = this
  , type = dialect === 'mysql' ? 'signed' : 'integer'
  , match = false;
  return this.User.create({
    intVal: this.sequelize.cast('1', type)
  }, {
    logging: function(sql) {
      expect(sql).to.match(new RegExp("CAST\\(N?'1' AS " + type.toUpperCase() + '\\)'));
      match = true;
    }
  }).then(function(user) {
    
    ...

    });
  });

  [Boolean]

  // 初始化省市区数据
    Models.a.findOne({where:{id:1},logging:false}).then(function(area){
      if(area) return console.log("> ....exists!")
    })

   ```


## sequelize.bulkCreate   

- bulkCreate 创建 并且插入数据  
- aaa 是对象数组  
  ```
  var  aaa = [
    {'id':1,'title':'一个例子','content':'栗子内容'}
  ]
  Models.provinces.bulkCreate(aaa,{logging:false}).then(function (result) {
    console.log(">  OK!")
  }).catch(function (err) {
    console.log("> ..-> error :",err)
  });
  ```

## sequelize建表

 ```
 var sequelize = require('db/json') //连数据库
 var Sequelize = require('sequelize');
 var User = sequelize.define('User',{
    user_id:{ type:Sequelize.STRING,primaryKey:true },
    name: Sequelize.STRING,    
    phone: Sequelize.STRING,    
    create_date: Sequelize.DATE,    
    update_date: Sequelize.DATE   
 },{
    freezeTableName:true,  //默认false修改表名为复数，true不修改表名,与数据库表名同步
    tableName:'user',
    timestamps:false
 })
 ```

 

## setDataValue,getDataValue

```
var name = '张三'
sequelize.aa.findOne({
  where:{...}
}).then(function(result){
  var a = result.getDataValue('name')
  var b = ressult.setDataValue('name':name)
})

```
