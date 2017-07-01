# TTY

- tty 模块主要提供了tty.ReadSream和tty.WriteStream这两个类  
- TTY 上下文中,process.stdin是 tty.ReadStream实例, process.stdout是 tty.WriteStream实例  

```
 const isInteractive = process.stdout.isTTY;
```

