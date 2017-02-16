
ElasticSearch是一个基于Lucene的搜索服务器。它提供了一个分布式多用户能力的全文搜索引擎，基于RESTful web接口。Elasticsearch是用Java开发的，并作为Apache许可条款下的开放源码发布，是当前流行的企业级搜索引擎。设计用于云计算中，能够达到实时搜索，稳定，可靠，快速，安装使用方便.

Lucene的目的是为软件开发人员提供一个简单易用的工具包    ,信息检索程序库

RESTful web: 
    REST是一种架构风格，其核心是面向资源，REST专门针对网络应用设计和开发方式，以降低开发的复杂性，提高系统的可伸缩性。REST提出设计概念和准则为：
        1.网络上的所有事物都可以被抽象为资源(resource)
        2.每一个资源都有唯一的资源标识(resource identifier)，对资源的操作不会改变这些标识
        3.所有的操作都是无状态的

# 目录
- [搜索](#搜索)

> Method:GET `/api/search?keyword=00&type=0 ` 客户端接口
> <type>  = 搜索类型 “0”用户搜索; “1”会议搜索; “2”工位搜索; “3”订单搜索; “4”首页广告搜索
> <keyword> = 用户输入的关键字
  type = 0       keyword 可根据用户        ［电话号码，用户名，昵称］查询 
  type = 1 || 2  keyword 可根据 会议或工位的 [发布状态，标题关键字，详情关键字，用户名，电话号码，所在省份，所在地级市，详细地址关键字] 查询
  type = 3       keyword 可根据 订单        [订单编号,订单标题，订单类型，支付编号，订单状态] 查询
  type = 4       keyword 可根据 广告        [发布状态，广告标题，广告详情，广告商品编号] 查询


> token   = eyJhbGciOiJIUzI1NiJ9.MQ.6z44GClzAsUED1M_UyxqdREdDKcYFnL9tSqd5ZhLhsY

**callback**

```js
{
    "code": 0,
    "message": "获取用户信息成功！",
    "data": [
        {
            "id": 3,
            "user_id": 3,
            "sex": 1,
            "type": 0,
            "status": 0,
            "name": "000000",
            "head_url": "/img/3YbfRt74JW14798879347791.jpg",
            "nikename": "000",
            "mailbox": "123123@qq.com",
            "telphone": "",
            "address": "",
            "region": "",
            "zipcode": "",
            "id_number": "",
            "create_at": "2016-11-23 15:58:58",
            "update_at": "2016-11-28 09:29:08"
        },
        {
            "id": 6,
            "user_id": 6,
            "sex": 0,
            "type": 0,
            "status": 0,
            "name": "000",
            "head_url": "",
            "nikename": "",
            "mailbox": "",
            "telphone": "",
            "address": "",
            "region": "",
            "zipcode": "",
            "id_number": "",
            "create_at": "2016-12-09T01:52:04.582Z",
            "update_at": "2017-01-04T08:06:04.480Z"
        }
    ] 
}
```


parse() 方法可解析一个日期时间字符串，并返回 1970/1/1 午夜距离该日期时间的毫秒数。

语法

Date.parse(datestring)

> Method: 循环同一个搜索   time_test
```
time_test:function(sql,total_sql,t){
        var t1 = (new Date()).valueOf();
         console.log('t1',t1);
        for ( var i=0;i<t;i++){
            this.mysql_search(sql,total_sql);
        }
        var t2 = (new Date()).valueOf();
        console.log('t2',t2);
        return t2-t1;
    }
```

MySQL一般认为，利用索引不能过滤75%以上的数据则不走索引
源码中是有一个公式计算的，不一定75%，但是在这个区间浮动，70%~85%的过滤下限都有可能，依赖于索引的长度



全表搜索 （select * from ...）result:
10万次  用时   1100ms ~ 1500ms


模糊查询在mysql myisam,innodb引擎中走的是全表扫描；
曾经尝试过5KW的数据总量，1000万，2000万，3000万，4000W偏移时，运行时间分别维持在11S、15S、20S、16S左右。单线程对单CPU的使用率很高，cpu消耗近100%。





0.对查询进行优化，应尽量避免全表扫描，首先应考虑在 where 及 order by 涉及的列上建立索引。
1.应尽量避免在 where 子句中对字段进行 null 值判断，否则将导致引擎放弃使用索引而进行全表扫描

2.应尽量避免在 where 子句中使用!=或<>操作符，否则将引擎放弃使用索引而进行全表扫描。

3.应尽量避免在 where 子句中使用 or 来连接条件，否则将导致引擎放弃使用索引而进行全表扫描
select id from t where num=10 or Name = 'admin'
可以这样查询：

select id from t where num = 10
union all
select id from t where Name = 'admin'




4.in 和 not in 也要慎用，否则会导致全表扫描，如：
　　select id from t where num in(1，2，3)
　　对于连续的数值，能用 between 就不要用 in 了：
　　select id from t where num between 1 and 3

5.下面的查询也将导致全表扫描：
　　select id from t where name like '%abc%'
　　若要提高效率，可以考虑全文检索。
    alter table `meeting` add fulltext zzx_title_fc(`title`); 
    SELECT title FROM  `meeting`  WHERE MATCH (title)  AGAINST( 'qqqqq' IN BOOLEAN MODE)  >>>这里的qqqqq必须时表里有的必需写全,如果输入qq则无法搜索到 ;;然而用like 搜索无论输入qqqqq还是qq都能搜索到


6.如果在 where 子句中使用参数，也会导致全表扫描。因为SQL只有在运行时才会解析局部变量，但优化程序不能将访问计划的选择推迟到运行时;它必须在编译时进行选择。然而，如果在编译时建立访问计划，变量的值还是未知的，因而无法作为索引选择的输入项。如下面语句将进行全表扫描：
　　select id from t wherenum=@num
　　可以改为强制查询使用索引：
　　select id from t with(index(索引名)) wherenum= @num
7.应尽量避免在 where 子句中对字段进行表达式操作，这将导致引擎放弃使用索引而进行全表扫描。如：
　　select id from t where num/2=100
　　应改为：
　　select id from t where num=100*2

8.应尽量避免在where子句中对字段进行函数操作，这将导致引擎放弃使用索引而进行全表扫描。如：
　　select id from t where substring(name，1，3)='abc'--name以abc开头的id
　　select id from t where datediff(day，createdate，'2005-11-30')=0--‘2005-11-30’生成的id
    很多时候用 exists 代替 in 是一个好的选择：
    select num from a where num in(select num from b)
    用下面的语句替换：
    select num from a where exists(select 1 from b where num=a.num)

9.最好不要给数据库留NULL，尽可能的使用 NOT NULL填充数据库.
  备注、描述、评论之类的可以设置为 NULL，其他的，最好不要使用NULL。
  空 真空杯子  和  null 装满空气杯子
  可以在num上设置默认值0，确保表中num列没有null值，然后这样查询：
    select id from t where num = 0

10.不要在 where 子句中的“=”左边进行函数、算术运算或其他表达式运算，否则系统将可能无法正确使用索引。

11.在使用索引字段作为条件时，如果该索引是复合索引，那么必须使用到该索引中的第一个字段作为条件时才能保证系统使用该索引，否则该索引将不会被使用，并且应尽可能的让字段顺序与索引顺序相一致。


12.不要写一些没有意义的查询，如需要生成一个空表结构：

    select col1,col2 into #t from t where 1=0
    这类代码不会返回任何结果集，但是会消耗系统资源的，应改成这样：

    create table #t(…)

13.Update 语句，如果只更改1、2个字段，不要Update全部字段，否则频繁调用会引起明显的性能消耗，同时带来大量日志。

14.对于多张大数据量（这里几百条就算大了）的表JOIN，要先分页再JOIN，否则逻辑读会很高，性能很差。

15.select count(*) from table；这样不带任何条件的count会引起全表扫描，并且没有任何业务意义，是一定要杜绝的。

16.索引并不是越多越好，索引固然可以提高相应的 select 的效率，但同时也降低了 insert 及 update 的效率，因为 insert 或 update 时有可能会重建索引，所以怎样建索引需要慎重考虑，视具体情况而定。一个表的索引数最好不要超过6个，若太多则应考虑一些不常使用到的列上建的索引是否有 必要。


17.应尽可能的避免更新 clustered 索引数据列，因为 clustered 索引数据列的顺序就是表记录的物理存储顺序，一旦该列值改变将导致整个表记录的顺序的调整，会耗费相当大的资源。若应用系统需要频繁更新 clustered 索引数据列，那么需要考虑是否应将该索引建为 clustered 索引。
(clustered 指的是聚集索引,索引可分聚集和非聚集索引，这两者区别比较多，但是最主要的区别是：
一个表的聚集索引只能有一个，是因为数据行在保存的时候，是按聚集索引的顺序保存的，你可以把它简单的理解成物理存储的位置，这里涉及到页面的概念，你可以查查看。就是物理磁盘上分很多页面，一个有聚集索引的表，他的页面链是按聚集索引排列的，举个例子，如果一个页面已经写满了数据，你要插入一行，如果是非聚集索引，sql会随便找个地方保存，把地址记录进索引，但是如果是聚集索引，会把数据插入到这个页面，而后面的数据同时会往后移动(用页面拆分的办法)，看上去速度要慢，但是聚集索引在搜索时，速度会比非聚集索引快，因为他们是物理排序的

指定为 PRIMARY KEY 或 UNIQUE 约束创建聚集或非聚集索引。PRIMARY KEY 约束默认为 CLUSTERED；UNIQUE 约束默认为 NONCLUSTERED。如果表中已存在聚集约束或索引，那么在 ALTER TABLE 中就不能指定 CLUSTERED。如果表中已存在聚集约束或索引，PRIMARY KEY 约束默认为 NONCLUSTERED。)


18.尽量使用数字型字段，若只含数值信息的字段尽量不要设计为字符型，这会降低查询和连接的性能，并会增加存储开销。这是因为引擎在处理查询和连 接时会逐个比较字符串中每一个字符，而对于数字型而言只需要比较一次就够了。

19.尽可能的使用 varchar/nvarchar 代替 char/nchar ，因为首先变长字段存储空间小，可以节省存储空间，其次对于查询来说，在一个相对较小的字段内搜索效率显然要高些。

20.任何地方都不要使用 select * from t ，用具体的字段列表代替“*”，不要返回用不到的任何字段。

21.尽量使用表变量来代替临时表。如果表变量包含大量数据，请注意索引非常有限（只有主键索引）。

22. 避免频繁创建和删除临时表，以减少系统表资源的消耗。临时表并不是不可使用，适当地使用它们可以使某些例程更有效，例如，当需要重复引用大型表或常用表中的某个数据集时。但是，对于一次性事件， 最好使用导出表。

23.在新建临时表时，如果一次性插入数据量很大，那么可以使用 select into 代替 create table，避免造成大量 log ，以提高速度；如果数据量不大，为了缓和系统表的资源，应先create table，然后insert。

24.如果使用到了临时表，在存储过程的最后务必将所有的临时表显式删除，先 truncate table ，然后 drop table ，这样可以避免系统表的较长时间锁定。

25.尽量避免使用游标，因为游标的效率较差，如果游标操作的数据超过1万行，那么就应该考虑改写。

26.使用基于游标的方法或临时表方法之前，应先寻找基于集的解决方案来解决问题，基于集的方法通常更有效。

27.与临时表一样，游标并不是不可使用。对小型数据集使用 FAST_FORWARD 游标通常要优于其他逐行处理方法，尤其是在必须引用几个表才能获得所需的数据时。在结果集中包括“合计”的例程通常要比使用游标执行的速度快。如果开发时 间允许，基于游标的方法和基于集的方法都可以尝试一下，看哪一种方法的效果更好。

28.在所有的存储过程和触发器的开始处设置 SET NOCOUNT ON ，在结束时设置 SET NOCOUNT OFF 。无需在执行存储过程和触发器的每个语句后向客户端发送 DONE_IN_PROC 消息。

29.尽量避免大事务操作，提高系统并发能力。

30.尽量避免向客户端返回大数据量，若数据量过大，应该考虑相应需求是否合理。

实际案例分析：拆分大的 DELETE 或INSERT 语句，批量提交SQL语句

如果你需要在一个在线的网站上去执行一个大的 DELETE 或 INSERT 查询，你需要非常小心，要避免你的操作让你的整个网站停止相应。因为这两个操作是会锁表的，表一锁住了，别的操作都进不来了。

Apache 会有很多的子进程或线程。所以，其工作起来相当有效率，而我们的服务器也不希望有太多的子进程，线程和数据库链接，这是极大的占服务器资源的事情，尤其是内存。

如果你把你的表锁上一段时间，比如30秒钟，那么对于一个有很高访问量的站点来说，这30秒所积累的访问进程/线程，数据库链接，打开的文件数，可能不仅仅会让你的WEB服务崩溃，还可能会让你的整台服务器马上挂了。

所以，如果你有一个大的处理，你一定把其拆分，使用 LIMIT oracle(rownum),sqlserver(top)条件是一个好的方法。下面是一个mysql示例：

 

 
while(1){

 //每次只做1000条

 mysql_query(“delete from logs where log_date <= ’2012-11-01’ limit 1000”);

 if(mysql_affected_rows() == 0){

 //删除完成，退出！
 break；
}

//每次暂停一段时间，释放表让其他进程/线程访问。
usleep(50000)

}



用字段搜索 比 ＊ 全局搜索 快0.1秒左右




