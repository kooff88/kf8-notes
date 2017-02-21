# 目录

- [索引](#索引)
    -[建立索引的时机](#建立索引的时机)
    -[建立存储过程](#建立存储过程)
    -[索引建立删除](#索引建立删除)
- [搜索速度测试](#搜索速度测试)
- [配置文件改动](#配置文件改动)
- [sql语句书写方式](#sql语句书写方式)
- [UNSIGNED](#UNSIGNED)
# 索引
    - 建立索引的时机

    例如一两千条甚至只有几百条记录的表，没必要建索引，让查询做全表扫描就好了。
    至于多少条记录才算多，这个个人有个人的看法，我个人的经验是以2000作为分界线，记录数不超过 2000可以考虑不建索引，超过2000条可以酌情考虑索引。
    另一种不建议建索引的情况是索引的选择性较低。所谓索引的选择性（Selectivity），是指不重复的索引值（也叫基数，Cardinality）与表记录数（#T）的比值：

    Index Selectivity = Cardinality / #T
    显然选择性的取值范围为(0, 1]，选择性越高的索引价值越大，这是由B+Tree的性质决定的。
    例如，上文用到的employees.titles表，如果title字段经常被单独查询，是否需要建索引，我们看一下它的选择性：
    SELECT count(DISTINCT(title))/count(*) AS Selectivity FROM meeting;

    主键索引建立的规则是 int优于varchar,一般在建表的时候创建,最好是与表的其他字段不相关的列或者是业务不相关的列.
    一般会设为 int 而且是 AUTO_INCREMENT自增类型的

    在WHERE和JOIN中出现的列需要建立索引，但也不完全如此：
    MySQL只对<，<=，=，>，>=，BETWEEN，IN使用索引
    某些时候的LIKE也会使用索引。
    在LIKE以通配符%和_开头作查询时，MySQL不会使用索引。

    SELECT * FROM mytable WHERE username like'admin%'; -- 而下句就不会使用：
    SELECT * FROM mytable WHEREt Name like'%admin'; -- 因此，在使用LIKE时应注意以上的区别。

        索引的注意事项：
          索引不会包含有NULL值的列
          使用短索引
          不要在列上进行运算 索引会失效
          
          
          
        索引的本质：
          MySQL官方对索引的定义为：索引（Index）是帮助MySQL高效获取数据的数据结构。提取句子主干，就可以得到索引的本质：索引是数据结构。

   
    - 建立存储过程
        > 1.查询当前数据库有哪些存储过程
            show procedure status where Db="test";
          2.调用存储过程
            call myproce();      


        ```
       delimiter //
        create procedure myproce1()
        begin
        declare num int;
            set num = 1;
            while  num<1000  do
                 insert into meeting (user_id,statu,title,description,location,number_people,weeks,time_start,time_end,price,pic_url,contacts,telphone,province,city,street,area,facility_describe,invoice,deleted,create_at,update_at)
                 value('1','3','666','8888888','7777777','55','4','56','446','665','/img/YdnwH8ZAky14835020308581.jpg','uuu','13101111111','湖南市','邵阳市','asdasd','1231','qew','0','0',CURRENT_TIMESTAMP,CURRENT_TIMESTAMP);

            set num= num+1;
            end while;
        end//
        
        ```

    - 索引建立删除   
        ```
        建立索引
       ALTER TABLE meeting add INDEX title_index(title);

       删除索引
       ALTER TABLE meeting drop INDEX title_index(title);
        ```


# 搜索速度测试

 table:  meeting
 数据库数据：10000条
 点击次数 ：5次
 mysql搜索时间 time(ms): 961  769  838  854  753  平均: 835  ms
 存入redis中   time(ms): 30   48   42   37   24   平均: 36.2  ms

 数据量很少  但可以很明显看出效率了


# sql语句导入 需要配置文件改动

    1. sudo touch /etc/my.cnf
    2. sudo vim etm/my.cnf

    进入文件加入以下内容


    [client]
    default-character-set = utf8mb4

    [mysql]
    default-character-set = utf8mb4

    [mysqld]
    character-set-client-handshake = FALSE
    character-set-server = utf8mb4
    collation-server = utf8mb4_unicode_ci


    sql_mode=NO_ENGINE_SUBSTITUTION,STRICT_TRANS_TABLES

    3. 重起mysql
    4. 导入sql 文件

# node中 sql语句书写方式

    var query = 'id,pic_url,title,description,price,statu,update_at'
    var where = `WHERE user_id=${uid+statu}`;
    var sql = `select ${query},1 as type from meeting ${where} UNION select ${query},2 as type from station ${where} `;
    a和 b 表: SELECT COUNT(1) AS totals FROM  a s,b u where s.user_id=u.user_id  and s.statu in (0,1,2) and s.deleted=0



# UNSIGNED

    UNSIGNED属性就是将数字类型无符号化，与C、C++这些程序语言中的unsigned含义相同。例如，INT的类型范围是-2 147 483 648 ～ 2 147 483 647， INT UNSIGNED的范围类型就是0 ～ 4 294 967 295
    在MYSQL中整型范围：

    类型                 大小            范围（有符号）                              范围（无符号） 用途
    TINYINT           1 字节    (-128，127)                                    (0，255) 小整数值
    SMALLINT          2 字节    (-32 768，32 767)                              (0，65 535) 大整数值
    MEDIUMINT         3 字节    (-8 388 608，8 388 607)                        (0，16 777 215) 大整数值
    INT或INTEGER      4 字节    (-2 147 483 648，2 147 483 647)               (0，4 294 967 295) 大整数值




