# 提交规则 

- 每次提交，Commit message 都包括三个部分: Header, Body 和 Footer.

```
  <type>(<scope>): <subject>
  // 空一行
  <body>
  // 空一行
  <footer>
```

其中Header是必须的 ,Body和Footer可以省略  
任何一行都不得超过72个字符（或100个字符）。   


- Header  
  Header 部分只有一行，包括三个字段：type(必需),scope(可选) 和 subject(必需)  

type 用于说明commit 的类别，只允许使用下面7个标识.  

```
  feat(AAA) : 新功能(feature)
  fix(AAA) : 修补bug
  docs : 文档(documentation)
  style : 格式(不影响代码运行的变动)
  refactor:重构(即不是新增功能，也不是修改bug的代码变动)
  test:增加测试
  chore: 构建过程或辅助工具的变动
  revert: 撤销
  close : 关闭issue
  clean : 清理
```

- 如果type 为 feat和fix,则该commit 将肯定出现在Change log之中。   
  docs、chore、style、refactor、test）由你决定，要不要放入 Change log，建议是不要。  

