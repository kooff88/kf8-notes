# 目录 

-[subl ./打开sublime](#subl ./打开sublime)
-[安装插件](#安装插件)


# subl ./打开sublime

-  此命令可搞定
   ```
   alias subl=\''/Applications/Sublime Text.app/Contents/SharedSupport/bin/subl'\' ;

   ln -s "/Applications/Sublime Text.app/Contents/SharedSupport/bin/subl" /usr/local/bin/sublime
   ```

- 修改配置文件  永久使用subl ./
  ```
  1.vim ~/.bash-profile    /   vim ~/.zshrc
  
  在文件.bash-profile中添加软链接
  alias subl=\''/Applications/Sublime Text.app/Contents/SharedSupport/bin/subl'\' ;


  2.source ~/.bash-profile   (更新刚配置的环境变量)
  ```




# 安装插件

 1. control + ~
 2. command+shift+p    加载 Package Control:install Package
 3. 安装想要的插件