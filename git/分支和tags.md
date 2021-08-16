# git tags 和 branches 区别


```
tag 就像是一个里程碑一个标志一个点，branch 是一个新的 征程一条线；

tag 是静态的，branch 要向前走。

稳定版本备份用tag, 新功能多人开发用 branch (开发完成后merge到主分支)。

```


```
简单说比如 branch有1.0，1.1等，其中1.0分支里可以有1.0.1，1.0.2这些tag
```

```
tag 对应某次 commit, 是一个点，是不可移动的。branch 对应一系列 commit，是很多点连成的一根线，有一个HEAD 指针，是可以依靠 HEAD 指针移动的。所以，两者的区别决定了使用方式，改动代码用 branch ,不改动只查看用 tag。

```