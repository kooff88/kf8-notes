# 样式书写规范

- CSS样式一些规则  
  
##编码设置

```
 @charset "utf-8";
```

## 命名空间规范

- 布局:以g为命名空间，例如: .g-wrap, .g-header, .g-content   
- 状态:以s为命名空间,表示动态的，具有交互性质的状态,例如:.s-current, .s-selected   
- 工具:以u为命名空间，表示不耦合业务逻辑的，可复用的工具，例如：u-clearfix,u-dropMenu    
- 组件:以m为命名空间,以m为命名空间,表示可复用的，移植的组件模块，例如 m-slider,m-dropMenu   
- 钩子:以j为命名空间，以j为命名空间，表示特定给javascript调用的类名，例如:j-request,j-open    

