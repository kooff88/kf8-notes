# 目录

-[vue.js和express已有项目结合](#vue.js和express已有项目结合)
-[一些用到的sdk](#一些用到的sdk)
-[node中使用ajax一些术语](#node中使用ajax一些术语)

# vue.js和express已有项目结合

# 一些用到的sdk

  superagent :
       SuperAgent是轻量级更为优化的ajax API，对比大量糟糕的现存的API，SuperAgent是灵活的、易读的、并且非常易学，同时SuperAgent可用于Node.js！
        ```
        request
           .post('/api/pet')
           .send({ name: 'Manny', species: 'cat' })
           .set('X-API-Key', 'foobar')
           .set('Accept', 'application/json')
           .end(function(err, res){
             if (err || !res.ok) {
               alert('Oh no! error');
             } else {
               alert('yay got ' + JSON.stringify(res.body));
             }
           });
        ```
        原文地址 [https://github.com/visionmedia/superagent](#https://github.com/visionmedia/superagent)

   path:
   
# node中使用ajax一些术语

     req.end: