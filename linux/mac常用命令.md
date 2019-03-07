# 目录

- [mac关闭指定端口](#mac关闭指定端口)
- [nohup](#nohup)

## mac关闭指定端口

- 先执行如下命令  

```
  losf -i:端口号
```

- 会有类似下面的结果  

```
COMMAND     PID       USER   FD   TYPE             DEVICE SIZE/OFF NODE NAME
WebProces 42624 davidzhang    5u  IPv4 0x907152bbf7b2a875      0t0  TCP localhost:64438->localhost:radan-http (ESTABLISHED)
WebProces 42624 davidzhang   10u  IPv4 0x907152bbf7b64a05      0t0  TCP localhost:64439->localhost:radan-http (ESTABLISHED)
```

- 然后执行  

```
kill -9 42624
```

- 借宿进程就搞定了  


## nohup

挂载运行  

```
例如 启动一个node项目

nohup npm start &

tail -1000f nohup.out

```

