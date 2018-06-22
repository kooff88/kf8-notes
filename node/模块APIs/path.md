# Path

node的path模块  

1. 路径解析，得到规范化的路径格式。  

```
  // 对windows系统，目录分隔为'\', 对UNIX系统，分隔符为'/',针对'..'返回上一级；/与\\都被统一转换// path.normalize(p);

  var myPath = path.normalize(__dirname + '/test/a//b//../c/utilyou.mp3');
  console.log(myPath); //windows: E:\workspace\NodeJS\app\fs\test\a\c\utilyou.mp3
```

2. 路径结合，合并，路径最后不会带目录分隔符。  

```
  var path1 = 'path1',
      path2 = 'path2//pp\\',
      path3 = '../path3';

  var myPath = path.join(path1,path2,path3);
  console.log(myPath); // path1\path2\path3
```

3. 获取绝对路径  

```
  // path.resolve(path1,[path2]..[pathn]);

  // 以应用程序为起点，根据参数字符串解析出一个绝对路径

  /**
   * path 必须至少一个路径字符串值
   * [pathn] 可选路径字符串
   */

  var myPath = path.resolve('path1','path2','a/b\\c/');
  console.log(myPath);  // E:\workspace\NodeJS\path1\path2\a\b\c;
```


4. 获取相对路径

```
  // path.relative(from,to);
  // 获取两路径之间的相对关系

  /**
   * from 当前路径，并且方法返回值是基于from指定到to的相对路径
   * to   到哪路径，
   */


  var from = 'c:\\from\\a\\';
      to = 'c:/test/b';

  var _path = path.relative(from,to);

  console.log(_path);  // ..\..\test\b;  表示从from到to的相对路径
```

5. path.dirname(p)

```
  // 获取路径中目录名

  var myPath = path.dirname(__dirname + 'test/util you.mp3');
  console.log(myPath);
```

6. path.basename(path,[ext])

```
  // 获取路径中文件名，后缀是可选的，如果加，请使用'.ext'方式来匹配，则返回之中不包括后缀名； 
  var myPath = path.basename(__dirname + '/test/util you.mp3', '.mp3')
```

7. path.extname(path)

```
  // 获取路径中的扩展名。如果没有'.',则返回空
```

8. path.sep属性

```
 // 返回操作系统中文件分隔符；window是'\\',Unix是'/'
```

9. path.delimiter属性

```
  // 返回操作系统中目录分隔符，如window是';',Unix中是':'
```


## 属性

|序号|属性&描述|
|------|-------|
| 1 |path.sep => 平台的文件路径分隔符， '\\'或 '/'|
| 2 |path.delimiter => 平台的分隔符,; or ':'|
| 2 |path.posix => 提供上述path的方法，不过总是以posix兼容的方式交互|
| 2 |path.win32 => 提供上述path的方法，不过总是以win32兼容的方式交互|

