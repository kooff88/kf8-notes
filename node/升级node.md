# 升级node

1. 第一步：查看版本  
   node -v 
  
2. 第二步：清除node.js 的cache  
  sudo npm cache clean -f   

3. 第三步：安装 n 工具,这个工具是专门用来管理node.js的，别怀疑这个工具的名字，是他是他就是他，他的名字就是"n"  
  sudo npm install -g n  

4. 第四步：安装最新版本的node.js  
  sudo n stable  

5. 再次查看本机的node.js版本  
   node -v  
