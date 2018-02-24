# gh-pages

### 依赖包

gh-pages

### 命令

关键：  gh-pages -d -r 项目地址  

package.json  
```json
{
  "name": "项目一",
  "private": true,
  "scripts": {
    "build": "roadhog build",
    "deploy": "npm run build && gh-pages -d dist -r 项目地址",
    "d": "gh-pages -d dist -r 项目地址",
  },
  "dependencies": {
    ...
    "gh-pages": "^1.1.0",
    ...
  }  
}

```

运行命令: npm run delpoy  
或者:  npm run build   
      npm run d   


ps: 所遇到的问题   

1. 上传的用户名和gitlab上的用户名必须保持一致    
2. 使用http格式的仓库地址  