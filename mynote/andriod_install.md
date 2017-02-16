# 目录


[JDK](JDK)
[android-studio](android-studio)
[模拟器安装](模拟器安装)
        
#  JDK 

  Mac上自带JDK但是版本比较旧，我安装的JDK1.8 通过java -version可以查看JDK版本
  下载地址：
  http://www.oracle.com/technetwork/cn/java/javase/downloads/jdk8-downloads-2133151-zhs.html
    
  JDK安装 (按照自己的电脑下载对应的版本，下载版本不匹配是无法安装的)
  可视化安装工具 按顺序下一步。。　即可  
  默认安装目录：/Library/Java/JavaVirtualMachines/

  配置JAVA_HOME环境变量

  vim ~/.bash_profile   
  (该命令打开配置文件进行修改)

     配置文件中添加：
        export JAVA_HOME=/Library/Java/JavaVirtualMachines/jdk1.8.0_111.jdk/Contents/Home 
        export PATH=$JAVA_HOME/bin:$PATH 
        export CLASSPATH=.:$JAVA_HOME/lib/dt.jar:$JAVA_HOME/lib/tools.jar

    source ~/.bash_profile (该命令表示立即使用)

    卸载
    在finder中查找JavaAppletPlugin.plugin 并删除
    sudo rm -rf /Library/PreferencesPanes/JavaControlPanel.prefPane
    sudo rm -rf /Library/Java/JavaVirtualMachines/*


# android-studio
    下载地址：
    http://www.android-studio.org/

    Android Studio安装
    下载好Android Studio 后一路OK安装就可以了.

    配置ANDROID_HOME 环境变量
    我是第三种方法所以在/Users/{YOUR_USER_NAME}/Library/Android/sdk下面
    vim ~/.bash_profile

    export ANDROID_HOME={YOUR_PATH}
    export PATH=$PATH:$ANDROID_HOME/tools:$ANDROID_HOME/platform-tools



    Android Studio卸载

    卸载Android Studio 在终端(terminal)执行以下命令

    rm -Rf /Applications/Android\ Studio.app
    rm -Rf ~/Library/Preferences/AndroidStudio*
    rm ~/Library/Preferences/com.google.android.studio.plist
    rm -Rf ~/Library/Application\ Support/AndroidStudio*
    rm -Rf ~/Library/Logs/AndroidStudio*
    rm -Rf ~/Library/Caches/AndroidStudio*
    删除Projects

    rm -Rf ~/AndroidStudioProjects

    删除gradle

    rm -Rf ~/.gradle

    卸载Android Virtual Devices(AVDs) and *.keystore

    注意：如果有其他IDE需要用到，请不要删除

    rm -Rf ~/.android

    删除Android SDK Tools

    注意：如果有其他IDE需要用到，请不要删除

    rm -Rf ~/Library/Android*


# 模拟器安装
   Android Stuido里面的AVD Manager可以创建模拟器，使用起来也比较简单，缺点就是性能不行，现在比较流行使用Genymotion，号称史上最快的Android模拟器。下面我们就来装Genymontion。 
     
      安装Virtual Box

      virtualbox.org

      注册用户
          进入Genymontion 官网注册用户 （需要邮箱认证）
          认证成功 进入Genymontion官网下载并安装 Genymotion

          安装Genymontion插件  












