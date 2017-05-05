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
