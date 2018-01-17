# npm

-[npm link](#npm link)  

## npm link

创建快捷链接，供本地模块调试使用（比复制好操作）。  

1. 创建开发模块的短链接   

  首先，在模块目录（src/myModule）下运行npm link命令。  

  > src/Mymodule$  npm link  
  
  上面的命令会在npm的全局模块目录内，生成一个符号链接文件，该文件的名字就是package.json文件中指定的文件名。  

  > /path/to/global/node_modules/myModule -> src/myModule  
  
  这个时候，已经可以全局调用myModule模块了，但是如果我们要让这个模块安装在项目内，还要进行洗面的步骤。  

2. 创建使用中项目的短链接  

  切换到项目目录，再次运行npm link， 并指定模块名。  

  > src/myProject$ npm link myModule  
  
  上面的命令等同于生成了本地模块的符号链接。  

  > src/myProject/node_modules/myModule -> /path/to/global/node_modules/myModule  
  
3. 删除link  

  如果你的项目不再需要该模块，可以在项目目录内使用npm unlink命令。删除符号链接。  

  > src/myProject$ npm unlink myModule  
  