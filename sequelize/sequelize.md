# 目录

[sequelize基本用法](#sequelize基本用法)

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


