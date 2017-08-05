# multer

- multer是express官方推荐的文件上传中间件，他是在busbody的基础上开发的.

#####配置

新建multerUtil.js

```
  var multer = require('multer');
  var storage = multer.diskStorage({
    //设置上传后文件路径，uploads文件夹会自动创建
    destination:function(req,file,cb){
      cd(null,'./public/uploads')
    },

    //给上传文件重命名，获取添加后缀名
    filename:function(req,file,cd){
      var fileFormate = (file.originalname).split('.');
      cb(null,file.fieldname + '-' + Date.now() + "." + fileFormat[fileFormat.length - 1]);
    }
  });

    //添加配置文件到multer对象
    var upload = multer({
      storage:storage
    });

    // 如果需要其他设置，请产考muler的limits
    /*
      var upload = multer({
        storage:storage,
        limits:{}
     })
    */

    module.exports = upload;
```

####  使用

testController.js

```
  var multer = require('./multerUtil');
   //multer有single()中的名称必须是表单上传字段的name名称
   var upload = multer.single('file');
   exports.dataInput = function(req,res){
    upload(req,res,function(err){
       //添加错误处理
        if (err) {
           return  console.log(err);
        }

        //文件信息在req.file或者req.file中显示
        console.log(req);        
    });
   }

```

app.js

```
  var tesController = require('./testController');

  app.post('./dataInput',testController.dataInput)
```
