# 目录

-[shell修改为zsh皮肤](#shell修改为zsh皮肤)


# shell修改为zsh皮肤

手动安装

  ```
   1.克隆仓库  
      git clone git ://github.com/robbyrussell/oh-my-zsh.git ~/.oh-my-zsh

   2.创建一个zsh的配置文件
     注意:如果你已经有一个 ~/.zshrc文件的话,建议你先做备份,使用以下命令
     cp ~/.zshrc ~/.zshrc.orig

   3.然后开始创建zsh的配置文件  
     cp ~/.oh-my-zsh/templates/zshrc.zsh-template ~/.zshrc   

   4.设置zsh为你的默认的shell  
  ```

 自动安装
 
  ```
  curl -fsSL https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh | sh


  wget https://raw.githubusercontent.com/robbyrussell/oh-my-zsh/master/tools/install.sh -O - | sh
  ```



 