# 目录  

- [CRLF](#CRLF)
- [thead,tbody,tfoot](#thead,tbody,tfoot)

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