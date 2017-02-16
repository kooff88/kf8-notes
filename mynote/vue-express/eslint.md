# 目录 

-[介绍](#介绍)
-[安装](#安装)


# 介绍

    EsLint帮助我们检查Javascript编程时的语法错误。比如：在Javascript应用中，你很难找到你漏泄的变量或者方法。EsLint能够帮助我们分析JS代码，找到bug并确保一定程度的JS语法书写的正确性。

    EsLint是建立在Esprima(ECMAScript解析架构)的基础上的。Esprima支持ES5.1,本身也是用ECMAScript编写的，用于多用途分析。EsLint不但提供一些默认的规则（可扩展），也提供用户自定义规则来约束我们写的Javascript代码。

    EsLint提供以下支持：

    ES6
    AngularJS
    JSX
    Style检查
    自定义错误和提示
    EsLint提供以下几种校验：

    语法错误校验
    不重要或丢失的标点符号，如分号
    没法运行到的代码块（使用过WebStorm的童鞋应该了解）
    未被使用的参数提醒
    漏掉的结束符，如}
    确保样式的统一规则，如sass或者less
    检查变量的命名


# 安装

    Npm install gulp-eslint –save-dev

    在你的项目目录下，运行：eslint –init将会产生一个.eslintrc的文件，文件内容包含一些校验规则

    ```
    {
        "rules": {
            "semi": ["error", "always"],
            "quotes": ["error", "double"]
        }
    }
    ```
    其中”semi”和”quotes”是规则名称。EsLint还提供了error的级别，对应数字，数字越高错误的提示越高，如0代码错误不提示、1代表警告提醒但不影响现有编译、2error会抛出错误。

    "extends": "eslint:recommended"
    Extends是EsLint默认推荐的验证，你可以使用配置选择哪些校验是你所需要的，可以登录[npmjs.com](#npmjs.com)查看









