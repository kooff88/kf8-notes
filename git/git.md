# 目录

- [git加载项目](#git加载项目)  
- [git第一次加载项目](#git第一次加载项目)  
- [git提交任务](#git提交任务)  
- [github与gitlab生成密钥](#github与gitlab生成密钥)  
- [github与gitlab同一电脑同时应用](#github与gitlab同一电脑同时应用)  
- [github代码提交](#github代码提交)  
- [gitlog日志](#gitlog日志)  
- [submodule](#submodule)  
- [ssh-add](#ssh-add)  

# git简单笔记

    git  用法

    上传 并且加载最新项目：

    git remote -v 查看远程仓库
    git remote add upstream git@12...........git  # 添加远程路径
    git remote remove origin    # 删除远程路径
    git remote -v
    git fetch upstream

    git checkout 
    git branch -av
    git checkout dev  切换分支到dev
    
    git merge upstream/dev （合并项目）

    git pull upstream 拉回上游分支

    git init   加载package.json 文件
    
    git fetch origin branchname:branchname    git拉取远程分支到本地分支或者创建本地新分支
    
    git push --set-upstream origin dev     //初次提交 需指定默认分支

    git pull origin dev --allow-unrelated-histories  (fatal: refusing to merge unrelated histories)
    
# git第一次加载项目

    git clone git@git.... 进行项目clone 
    subl ./ 用sublime打开项目 查看


    如果报错:
    The project you were looking for could not be found.
    repository 'https://.......' not found

    解决方案: git clone https://username:password@gitlab.com/xxx/xxx.git

# git提交任务

    git add . 
    git commit -m "描述"
    git remote add origin git@xx.xx.xx.xx:repos/xxx/xxx/xxx.git
    git push git push origin master

# github与gitlab生成密钥

    1. 密钥生成
    ssh-keygen -t rsa -C "zhangpeng101@163.com"
       
    2.密钥添加 
      subl /Users/mac/.ssh/id_rsa.pub（通过sublime打开显示公共密钥） 
      复制》》粘贴到github/gitlab公钥添加处》》
      
    3.设置远程仓库 即可
       git remote -v
       git remote add origin  git@140.206.185.170:666/wabg-server.git (这是github/gitlab中ssh地址，复制过来即可)

    other:
    ~   最外路径
    .ssh 进入密钥文件夹
    文件夹内包括config 配置文件   ；；各种密钥文件
    config      id_rsa      id_rsa.pub  id_rsa1     id_rsa1.pub known_hosts

    cat  id_rsa.pub (通过cat 命令打开密钥查看)




# github与gitlab同一电脑同时应用

    github与gitlab同一电脑同时应用

    生成密钥
        ssh-keygen -t rsa -C " 注册的gitlab邮箱"
        提示要输入名称，不管，一路回车，也不要设置密码
        ssh-keygen -t rsa -C " 注册的github邮箱"
        这次名称输入 id_rsa_github,路径保存在/Users/mac/.ssh/id_rsa_work
        ➜  ssh-keygen -t rsa -C "邮箱地址"
        Generating public/private rsa key pair.
        Enter file in which to save the key (/Users/mac/.ssh/id_rsa): /Users/mac/.ssh/id_rsa_work
        Enter passphrase (empty for no passphrase):
        Enter same passphrase again:
        Your identification has been saved in /Users/mac/.ssh/id_rsa_work.
        Your public key has been saved in /Users/mac/.ssh/id_rsa_work.pub.
        The key fingerprint is:
        SHA256:x23i+D537uEYJFSLlbCwPKGtOKni5wNASzku1H8idc8 597292454@qq.com
        The key's randomart image is:
        +---[RSA 2048]----+
        |  o     o ..o.   |
        | * . . = + =..   |
        |= o o o B + .    |
        |oo . = o E .     |
        |o   = + S = +    |
        | . . .   + =     |
        |. o     . . . .  |
        |.. o     .. .+.. |
        | .o..    .oo.++  |
        +----[SHA256]-----+


    添加ssh key 
        ~/.ssh  路径下分别有
            id_rsa
            id_rsa.pub 


    添加 config （主要原因：创建密钥用了其他名称命名，此情况下必须使用config !）
        在~/.ssh 下添加config 配置文件
    
    配置文件内容：
        Host gitlab.com
            HostName gitlab.com
            user:59729233323@qq.com
            IdentityFile ~/.ssh/id_rsa
        Host github.com
            HostName github.com
            user:zhang101@qq.com
            IdentityFile ~/.ssh/id_rsa_work

    vim config (进行读写配置文件)
    wq 保存退出

# github代码提交

    git add.
    git commit -m "aaa"
    git push origin master
    
    
# gitlog日志  

    git log   >>>>打印提交日志
    git show a7d4c2055ee5cf2de35fa6733f43b71b7d0fb348    查看某条日志   (哈希值)
  
    git reset --hard commit_id  >>>>彻底回退到某个版本，本地的源码也会变成上一个版本内容
  
    git reset --soft 回退到某个版本，只回退了commit的信息，不会恢复到index file 一级，如果还要提交，直接commit即可.


## submodule

```
    git submodule add --force '仓库地址' '路径'
    # 其中，仓库地址是指模块仓库地址,路径指将子模块放置在当前工程下的路径.
    # 注意:路径不能以 / 结尾 (会造成修改不生效) , 不能是现有工程已有的目录(不能顺利clone)
    git submodule init #初始化 submodule
    git submodule update # 更新submodule(必须在跟目录执行命令)
```

- 当使用git clone 下来的工程中带有submodule时，初始的时候，submodule的内容并不会自动下载下来的,此时需要执行命令:

```
 git submodule update --init --recursive # 下载的工程带有submodule
 git submodule foreach git pull # submodule 里有其他的 submodule 一次更新
 git submodule foreach git pull origin master # submodule 更新  --->submodule(子仓库) foreach(循环执行git pull origin master这一条命令)


 git submodule foreach --recursive git submodule init 
 git submodule foreach --recursive git submodule update
```


## ssh-add

ssh-add 命令是把专用密钥添加到ssh-agent的高速缓存中。  

该命令位置在 /usr/bin/ssh-add。



```
// 选项

    -D：删除ssh-agent中的所有密钥. 
    -d：从ssh-agent中的删除密钥 
    -e pkcs11：删除PKCS#11共享库pkcs1提供的钥匙。 
    -s pkcs11：添加PKCS#11共享库pkcs1提供的钥匙。 
    -L：显示ssh-agent中的公钥 
    -l：显示ssh-agent中的密钥 
    -t life：对加载的密钥设置超时时间，超时ssh-agent将自动卸载密钥 
    -X：对ssh-agent进行解锁 
    -x：对ssh-agent进行加锁

```
