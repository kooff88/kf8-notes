# nginx  Mac使用


1. 安装nginx   
	`brew install nginx`   


2. 启动 nginx   
  `sudo nginx`  


OK , nginx就安装好了, 可以在浏览器访问了，默认端口为8080,  在浏览器输入 http://localhost:8080/ 就能看到nginx在本计算机搭建的服务器。  


### 修改配置，反向代理静态页面

vim /usr/local/etc/nginx/nginx.conf  


```
# 自定义端口和映射本地网站路径
server {
	listen           5188;  #自定义端口
	server_name      localhost;

	location  /  {
		root   /Users/admin/......;  #本地网站文件夹路径
		index  index.html  index.htm;  #设置默认网页
	}
}
```

重启 nginx  

http://localhost:5188/   

