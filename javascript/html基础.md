# 目录  

- [CRLF](#CRLF)
- [thead,tbody,tfoot](#thead,tbody,tfoot)
- [colgroup标签](#colgroup标签)
- [label标签](#label标签)
- [kbd标签](#kbd标签)

## CRLF

```
  CRLF -- Carriage-Return Line-Feed 回车换行
```

## thead,tbody,tfoot

```
  <table border="1">
    <thead>
      <tr>
        <th>Month</th>
        <th>Savings</th>
      </tr>
    </thead>
    <tfoot>
      <tr>
        <td>Sum</td>
        <td>$180</td>
      </tr>
    </tfoot>

    <tbody>
      <tr>
        <td>January</td>
        <td>$100</td>
      </tr>
      <tr>
        <td>February</td>
        <td>$80</td>
      </tr>
    </tbody>
  </table>
```

- 字面理解分别是  表格的头，身体和脚。  
tbody 这个标签可以控制表格分行下载，可以让其中的内容比网页中别的东西(如图片)先下载下来  
这样可以让别人先看到网页的实质性的内容，不用等那么久了，在需要分行下载处加上<tbody>和</tbody>  

## colgroup

<colgroup>标签 用于对表格中的列进行组合，以便对其进行格式化。  
如需对全部列应用样式，<colgroup> 标签很有用，这样就不需要对各个单元和各行重复应用样式了。  
<colgroup> 标签只能在 table 元素中使用。  

```
<table width="100%" border="1">
  <colgroup span="2" align="left"></colgroup>
  <colgroup align="right" style="color:#0000FF;"></colgroup>
  <tr>
    <th>ISBN</th>
    <th>Title</th>
    <th>Price</th>
  </tr>
  <tr>
    <td>3476896</td>
    <td>My first HTML</td>
    <td>$53</td>
  </tr>
</table>
```


## label标签

在用户注册的时候，常常用户点击文字就需要将光标聚焦到对应的表单上面，依靠<label>标签的for属性可以实现  

```
...

  <table>
      <tr>
        <td><label for="username">用户名：</label></td>
        <td><input type='text' name='username' id='username' /></td>
      </tr>
      <tr>
        <td><label for="password">用户名：</label></td>
        <td><input type='password' name='password' id='password' /></td>
      </tr>
  </label>

...

```

## kbd标签

```
  <kbd> 标签定义键盘文本

  说到技术概念上的特殊样式时，既要提要<kbd>标签。正如你已经猜到的，它用来表示文本是从键盘上键入的。

  浏览器通常用等宽字体来显示改标签中包含的文本


  栗子:

  键入<kbd>quit</kbd> 来退出程序,或者键入<kbd>menu</kbd> 来返回主菜单。
```
