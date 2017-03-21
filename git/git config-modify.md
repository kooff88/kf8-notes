# 目录

-[git config --list](#git config --list)
-[git config](#git config)


## git config --list
  ```
  credential.helper=osxkeychain
  user.name=config
  user.email=zp@gmail.com
  core.repositoryformatversion=0
  core.filemode=true
  core.bare=false
  core.logallrefupdates=true
  core.ignorecase=true
  core.precomposeunicode=true
  remote.origin.url=git@git.gitlab.com:aa/aa.git
  remote.origin.fetch=+refs/heads/*:refs/remotes/origin/*
  branch.master.remote=origin
  branch.master.merge=refs/heads/master
  ```


## git config

  ```
  全局修改配置

  git config --global user.name "zp"
  git config --global user.email zp@gmail.com


  非全局修改

  git config  user.name "zp"
  git config  user.email zp@gmail.com
  ```

## 配置自动换行（自动转换坑太大）
  ```
  git config --global core.autocrlf input # 提交到git是自动将换行符转换为lf
  ```
  