# 笔记


[github与gitlab同一电脑同时应用](github与gitlab同一电脑同时应用)



github与gitlab同一电脑同时应用

生成密钥

    ssh-keygen -t rsa -C " 注册的gitlab邮箱"
    提示要输入名称，不管，一路回车，也不要设置密码

    ssh-keygen -t rsa -C " 注册的gitlab邮箱"
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
    ~/.ssh  路径下分别由

    id_rsa
    id_rsa.pub 


添加 config
     在~/.ssh 下添加config 配置文件
    
    配置文件内容：
    Host gitlab

            HostName gitlab.com
            IdentityFile ~/.ssh/id_rsa

    Host github
    
            HostName github.com
            IdentityFile ~/.ssh/id_rsa_work

                    













