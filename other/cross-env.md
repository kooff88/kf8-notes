# 目录 

-[cross-evn安装&使用](#cross-evn安装&使用)

# cross-evn安装&使用

```
  功夫不负有心人，在万能的google上，我找到了解决方法：cross-env。
  这个迷你的包能够提供一个设置环境变量的scripts，让你能够以unix方式设置环境变量，然后在windows上也能兼容运行。

```

- 安装cross-env:

  npm install cross-env --save-dev
  在NODE_ENV=xxxxxxx前面添加cross-env就可以了。

  ```例子
  "scripts": {
    "development": "cross-env NODE_ENV=development node ./bin/aaa",
  },
  ```
