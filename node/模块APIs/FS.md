# FS

Node.js文件I/O由标准POSIX函数包装后提供，每一个方法都有同步和异步两种形式，使用同步形式时，异常会被立即抛出，   
可以使用try/catch进行捕获处理，使用异步形式时，完成回调为最后一个参数，第一个参数为异常，并且可以为空。   

fs模块主要分为文件监控，文件流，文件信息。  

fs模块方法介绍，方法结尾为Sync的为同步方法，反之为异步方法，异步方法会有一个回调函数，且为最后一个参数，  
很多方法与linux中的文件方法一样。  

方法中参数介绍：  

- fd: 整数  
- file: 文件  
- path: 路径  
- data: 数据  
- callback: 回调函数  

|  方法  |   作用   |
|-------|---------|
| fs.access(path[,mode],callback) | 判断用户是否有权限操作给定的目录或者是文件 |
| fs.accessSync(path[,mode]) | 判断用户是否有权限操作给定的目录或者是文件  |
| fs.appendFile(file,data[,options],callback) | 将数据异步附加到文件  |
| fs.appendFileSync(file,data[,options] | 将数据同步附加到文件  |
| fs.chmod(path,mode,callback)  | 修改文件夹权限  |
| fs.chmodSync(path,uid,gid)  | 修改文件夹权限   |
| fs.chown(path,uid,gid,callback) | 更改文件夹的所有权  |
| fs.chownSync(path,uid,gid) | 更改文件夹的所有权  |
| fs.close(fd,callback)  | 关闭已打开的文件   |
| fs.closeSync(fd)  | 关闭已打开的文件   |
| fs.createReadStream(path[,options])  | 返回一个新的可读流对象   |
| fs.createWriteStream(path[,options])  | 返回一个新的可写流对象  |
| fs.fchmod(fd,mode,callback) | 更改文件权限  |
| fs.fchmodSync(fd,mode) | 更改文件权限  |
| fs.fchown(fd,uid,gid,callback)  | 更改文件所有权   |
| fs.fchownSync(fd,uid,gid)  | 更改文件所有权  |
| fs.fdatasync(fd,callback)  | 刷新数据到磁盘   |
| fs.fdatasyncSync(fd) | 刷行数据到磁盘 |
| fs.fstat(fd) | 返回文件的详细信息  |
| fs.fstatSync(fd) | 返回文件的详细信息  |
| fs.fsync(fd,callback) | 异步缓存数据到磁盘  |
| fs.fsyncSync(fd) | 同步缓存数据到磁盘  |
| fs.ftruncate(fd,len,callback) | 截取文件内容  |
| fs.ftruncateSync(fd,len) | 截取文件内容 |
| fs.futimes(fd,atime,callback) | 更改一个文件所提供的文件描述符引用的文件的时间戳  |
| fs.futimesSync(fd,atime,mtime) | 更改一个文件所提供的文件描述符引用的文件的时间戳  
| fs.lchmod(path,mode,callback) | 更改文件权限(不解析符号链接)  |
| fs.lchmodSync(path,mode) | 更改文件权限(不解析符号链接)  |
| fs.lchown(path,uid,gid,callback) | 更改文件所有权(不解析符号链接)  |
| fs.lchownSync(path,uid,gid) | 更改文件所有权(不解析符号链接)  |
| fs.link(existingPath,newPath,callback) | 创建硬链接（只能在本券中） |
| fs.linkSync(existingPath,newPath) | 创建硬链接（只能在本券中）  |
| fs.lstat(path,callback) | 获取文件信息（不解析符号链接）  |
| fs.lstatSync(path) | 获取文件信息（不解析符号链接） |
| fs.mkdir(path[,mode],callback) | 创建文件目录，如果目录已存在，将抛出异常  |
| fs.mkdirSync(path[,mode]) | 创建文件目录，如果目录已存在，将抛出异常  |
| fs.mkdtemp(prefix[,options],callback) | 创建临时目录  |
| fs.mkdtempSync(prefix[,options]) | 创建临时目录  |
| fs.open(path,flag[,mode],callback) | 打开文件  |
| fs.openSync(path,flags[,mode]) | 打开文件  |
| fs.read(fd,buffer,offset,length,position,callback) | 读取文件内容  |
| fs.readSync(path[,options]) | 读取文件内容  |
| fs.readdir(path[,options],callback) | 读取文件目录  |
| fs.readdirSync(path[,options]) | 读取文件目录  |
| fs.readFile(file[,options],callback) | 读取文件  |
| fs.readFileSync(file[,options]) | 读取文件  |
| fs.readlink(path[,options],callback) | 读取软链接信息  |
| fs.readlinkSync(path[,options]) | 读取软链接信息  |
| fs.rename(oldPath,newPath,callback) | 重命名路径  |
| fs.renameSync(oldPath,newPath) | 重命名路径  |
| fs.rmdir(path,callback) | 删除文件目录 |
| fs.rmdirSync(path,callback) | 删除文件目录  |
| fs.stat(path,callback) | 获取文件信息  |
| fs.statSync(path) | 获取文件信息  |
| fs.symlink(target,path[,type],callback) | 创建符号链接  |
| fs.symlinkSync(target,path[,type],callback) | 创建符号链接  |
| fs.truncate(path,len,callback) | 文件内容截取操作  |
| fs.truncateSync(path,len) | 文件内容截取操作  |
| fs.unlink(path,callback) | 删除文件操作  | 
| fs.unlinkSync(path) | 删除文件操作  |
| fs.unwatchFile(filename[,listener]) | 解除文件监控  |
| fs.untimes(path,atime,mtime,callback) | 修改文件时间戳  |
| fs.untimesSync(path,atime,mtime)  | 修改文件时间戳  |
| fs.watch(filename[,options][,listener]) | 监控文件 |
| fs.watchFile(filename[,options],listener) | 监控文件 |
| fs.write(fd,buffer,offset,length[,options]) | 向文件写数据  |
| fs.writeSync(fd,buffer,offset,length[,options]) | 向文件写数据  |
| fs.writeFile(file,data[,options],callback) |  向文件写数据 |
| fs.writeFileSync(file,data[,options]) |  向文件写数据 |
