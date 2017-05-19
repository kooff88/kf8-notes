# 目录

- [不存在null判断处理](#不存在null判断处理)


## 不存在null判断处理
```
    name::::::, { 
        type: 'VARCHAR(100)',
        allowNull: true,
        defaultValue: null,
        primaryKey: false 
    }

    错误写法:
     1.if(name.defaultValue=='null')...
     2.if(name.defaultValue=='')...
    正确写法:
     if(!name.defaultValue)...
```
INSERT INTO `charger` (`id`,`type`,`create_at`,`update_at`) VALUES (3,2,'2017-05-18 11:06:17','2017-05-18 11:06:17') ON DUPLICATE KEY UPDATE `id`=VALUES(`id`), `type`=VALUES(`type`), `update_at`=VALUES(`update_at`);