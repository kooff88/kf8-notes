# 目录 

-[SuperAgent介绍](#SuperAgent介绍)

# SuperAgent介绍

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