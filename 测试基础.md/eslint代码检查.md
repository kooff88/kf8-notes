# ESlint 代码检查

简介  
  ESlint是一个可扩展，每条规则独立，不内置编码风格为理念编写的一个lint工具.  

主要特点：  
  
1. 默认规则包含所有JSlint,JSHint 中存在的规则，易迁移。      
2. 规则可配置性高：可设置【警告】，【错误】两个提示级别，或者直接禁用.   
3. 包含代码风格检测的规则(可以丢掉JSCS了)  
4. 支持插件扩展，自定义规则  

(一)安装使用  
  npm install -g eslint  
(二)创建 .eslint 系统文件  
(三)根据需要添加ESlint配置  
    例如  "quotes":[2,"double"] >> 强制使用双引号  



### ESlint 校验级别

```
 0 - 不验证
 1 - 警告
 2 - 错误
```

### ESlint 校验规则

可在 .eslint 文件中添加推荐规则 "eslint:recommended";  如果自定义规则要将此规则去掉!    

规则说明：  
```
  "no-alert" : 0                            禁止使用alert confirm prompt
  "no-array-contructor":2                   禁止使用数组构造器
  "no-bitwise":0                            禁止使用按位运算符     
  "no-caller":1                             禁止使用argument.caller或者arguments.callee
  "no-catch-shadow":2                       禁止catch字句参数与外部作用域变量同名
  "no-class-assign":2                       禁止给类赋值
  "no-cond-assign":2                        禁止在条件表达式中使用赋值语句
  "no-console":2                            禁止使用console
  "no-const-assign":2                       禁止修改const声明的变量
  "no-constant-condition" :2                禁止在条件中使用常量表达式if(true) if(1)
  "no-continue":0                           禁止使用continue
  "no-control-regex":2                      禁止在正则表达式中使用控制字符
  "no-debugger":2                           禁止使用debugger
  "no-delete-var":2                         不能对var声明的变量使用delete操作符
  "no-div-regex":1                          不能使用看起来像除法的正则表达式 /=foo/
  "no-dupe-keys":2                          在创建对象字面量时不允许键重复{a:1,a:1}
  "no-dupe-args":2                          函数参数不能重复
  "no-duplicate-case":2                     switch中的case标签不能重复
  "no-else-return":2                        如果if语句里面有return,后面不能跟else语句
  "no-empty":2                              块语句中的内容不能为空
  "no-empty-character-class":2              正则表达式中的[]内容不能为空
  "no-empty-label":2                        禁止使用空label
  "no-eq-null":2                            禁止对null使用==或!=运算符
  "no-eval" : 1                             禁止使用eval
  "no-ex-assign":2                          禁止给catch语句中的异常参数赋值
  "no-extend-native":2                      禁止扩展native对象
  "no-extra-bind":2                         禁止不必要的绑定
  "no-extra-boolean-cast":2                 禁止不必要的bool转换
  "no-extra-parens":2                       禁止非必要的括号
  "no-extra-semi":2                         禁止多余的冒号
  "no-fallthrough":1                        禁止switch穿透  
  "no-floating-decimal":2                   禁止数字字面量中使用前导和末尾小数点   
  "no-func-assign":2                        禁止重复的函数声明
  "no-implicit-coercion":1                  禁止隐式转换
  "no-implicit-globals": 2                  禁止全局范围内使用var 和命名的function声明
  "no-implied-eval":2                       禁止隐式的eval
  "no-inline-comments":0                    禁止行内备注
  "no-inner-declarations":[2,"function"]    禁止在块语句中使用声明(变量或函数)
  "no-invalid-regexp":2                     禁止无效的正则表达式
  "no-invalid-this":2                       禁止无效的this,只能用在构造器，类，对象字面量
  "no-irregular-whitespace":2               不能有不规则的空格
  "no-iterator":2                           禁止使用iterator属性
  "no-label-var":2                          label名不能与var声明的变量名相同
  "no-labels":2                             禁止标签声明
  "no-lone-blocks":2                        禁止不必要的嵌套块
  "no-lonely-if":2                          禁止else语句内只有if语句
  "no-loop-func":1                          禁止在循环中使用函数(如果没有引用外部变量不形成闭包就可以)
  "no-mixed-requires":[0,false]             声明时不能混用声明类型
  "no-mixed-spaces-and-tabs":[2,false]      禁止混用tab和空格
  "linebreak-style" :[0,"windows"]          换行风格
  "no-multi-spaces":1                       不能用多余的空格
  "no-multi-str":2                          字符串不能用\换行
  "no-multiple-empty-lines":[1,{"max":2}]   空行最多不能超过2行
  "no-native-reassign":2                    不能重写native对象
  "no-negated-in-lhs":2                     in 操作符左边不能有
  "no-nested-ternary":0                     禁止使用嵌套的三目运算 
  "no-new":1                                禁止在使用new构造一个实例后不赋值
  "no-new-func":1                           禁止使用new Function
  "no-new-object":2                         禁止使用new Object()
  "no-new-require":2                        禁止使用new require
  "no-new-wrappers":2                       禁止使用new创建包装实例，new String new Boolean new Number
  "no-obj-calls":2                          不能调用内置的全局对象,比如Math() JSON()
  "no-octal":2                              禁止使用八进制数字
  "no-octal-escape":2                       禁止使用八进制转义序列
  "no-param-reassign":2                     禁止给参数重新赋值
  "no-path-concat":0                        node中不能使用__dirname或__filename做路径拼接
  "no-plusplus":0                           禁止使用++，-
  "no-process-env":0                        禁止使用process.env
  "no-process-exit":0                       禁止使用process.exit()
  "no-proto":2                              禁止使用proto属性
  "no-redeclare":2                          禁止重复声明变量
  "no-regex-spaces":2                       禁止在正则表达式字面量中使用多个空格 /foo bar/
  "no-restricted-modules":0                 如果禁用了指定模块，使用就会报错
  "no-return-assign":1                      return语句中不能有赋值表达式
  "no-script-url":0                         禁止使用javascript:void(0)
  "no-self-compare":2                       不能比较自身
  "no-sequences":0                          禁止使用逗号运算符
  "no-shadow":2                             外部作用域中的变量不能与它所包含的作用域中的变量或参数同名
  "no-shadow-restricted-names":2            严格模式中规定的限制标识符不能作为声明时的变量名使用
  "no-spaced-func":2                        函数调用时 函数名与()之间不能有空格
  "no-sparse-arrays":2                      禁止稀疏数组，[1,,2]
  "no-sync":0                               nodejs禁止同步方法
  "no-ternary":0                            禁止使用三目运算符
  "no-trailing-spaces":1                    一行结束后面不要有空格
  "no-this-before-super":0                  在调用super()之前不能使用this或super
  "no-throw-literal":2                      禁止抛出字面量错误throw "error"
  "no-undef":1                              不能有未定义的变量
  "no-undef-init":2                         变量初始化时不能直接给它赋值为undefined
  "no-undefined":2                          不能使用undefined
  "no-unexpected-multiline":2               避免多行表达式
  "no-underscore-dangle":1                  标识符不能以_开头或结尾
  "no-unneeded-ternary":2                   禁止不必要的嵌套  var isYes = answer === 1 ? true : false
  "no-unreadchable":2                       不能有无法执行的代码
  "no-unused-expressions":2                 禁止无用的表达式
  "no-unused-vars":[2,{"vars":"all","args","after-used"}] 不能有声明后未被使用的变量或参数
  "no-use-before-define":2                  未定义前不能使用
  "no-useless-call":2                       禁止不必要的call和apply
  "no-void":2                               禁止void操作符
  "no-var":0                                禁止var，用 let 和const 代替
  "no-warning-comments": [1, { “terms”: [“todo”, “fixme”, “xxx”], “location”: “start” }],//不能有警告备注 
  "no-with":2                               禁止用with
  "array-bracket-spacing":[2,"never"]       是否允许非空数组里面有多余的空格
  "arrow-parents":0                         箭头函数用小括号括起来
  "arrow-spacing":0                         => 的前/后括号
  "accessor-paris":0                        在对象中使用getter/setter
  "block-scoped-var":0                      块语句中使用var
  "brace-style":[1,"1tbs"]                  大括号风格
  "callback-return":1                       避免多次调用回调什么的
  "camelcase":2                             强制驼峰法命名
  "comma-dangle":[2,"never"]                对象字面量项尾不能有逗号
  "comma-spacing":0                         逗号前后的空格
  "comma-style":[2,"last"]                  逗号风格，换行时在行首还是在行尾
  "complexity":[0,11]                       循环复杂度
  "computed-property-spacing":[0,"never"]   是否允许计算后的键名什么的
  "consistent-return":0                     return 后面是否允许省略
  "consistent-this":[2,"that"]              this别名
  "constructor-super":0                     非派生类不能调用super,派生类必须调用super
  "curly":[2,"all"]                         必须使用if(){}中的{}
  "default-case":2                          switch语句最后必须有default
  "dot-location":0                          对象访问符的位置，换行的时候在行首还是在行尾
  "dot-notation":[0,{"allowKeywords":true}] 避免不必要的方括号
  "eol-last":0                              文件以单一的换行符结束
  "eqeqeq":2                                必须使用全等
  "func-names":0                            函数表达式必须有名字
  "func-style":[0,"declaration"]            函数风格，规定只能使用函数声明／函数表达式
  "generator-star-spacing":0                生成器函数*的前后空格
  "guard-for-in":0                          for in 循环要用if语句过滤
  "handle-callback-err":0                   nodejs处理错误
  "id-length":0                             变量名长度
  "indent":[2,4]                            缩进风格
  "init-declarations":  0                   声明时必须赋初始值

```


