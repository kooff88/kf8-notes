# 目录

[session管理器req.session.regenerate](#session管理器reqreq.session.regenerate)

## session管理器req.session.regenerate

```
    req.session.regenerate(function(){ 
        req.session.captcha = captcha.text;
        req.session.save();                      //保存一下修改后的Session
        req.set('Content-Type','image/svg+xml'); //在html中动态插入 svg +xml格式文件
        res.status(200).send(captcha.text);      //何种状态下发送什么信息
    })
```
