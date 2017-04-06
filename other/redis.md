# 目录

-[存储类型](#存储类型)
-[redis应用](#redis应用)
-[redis开启监听所有事件](#redis开启监听所有事件)

# 存储类型

    String
    Hash
    List
    Set
    Sorted set
    pub/sub
    Transactions

    注：
        从数据库取出的数据类型为已设置为json类型,存入redis时转换为string类型
        从redis中取出传回前端时 则转换为json类型 

    总结：运用redis缓存技术存储数据  减少了对数据库的重复查询 ，节省电脑资源，加快查询速度，提高搜索性能！！！
    总结：运用redis缓存技术存储数据  减少了对数据库的重复查询 ，节省电脑资源，加快查询速度，提高搜索性能！！！


#  redis应用
    ```
    引入:
    var redis={
            "host" :"110.0.0.1",
            "port" :"6380",
            "password" :"xxxxxx"
         }
    var redis_config = {
        "host": confRedis.host,
        "port": confRedis.port
    };
    var redisClient = redis.createClient(redis_config);
    var redisClient = redisClient;

    用法:
    redisClient.set('key',value);  //设置redis一条 record
    redisClient.expire('key',600);  //设置此条内容失效时间 十分钟

    // 获取redis此条内容 进行操作
    redisClient.get('key',function(err,reply){
       if(err) return res.json({code:19001,message:err });
       ... 
    }); 

    // 删除redis中此条内容
    redisClient.del('wabg-mss'+mobile,function(err,reply){
        if(reply||reply===0){
            return res.json({"code":0, "message":"删除成功！"});
        }
    })
    ```

## redis开启监听所有事件      
  
    开启命令: redis-cli -p 6380 config set notify-keyspace-events KEA
    redis-cli --csv psubscript '__key*__:*'  
    需要设置redis开启事件监听，默认未开启
    https://cnodejs.org/topic/5577b493c4e7fbea6e9a33c9  