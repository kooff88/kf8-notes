# DOM对象
-[Event对象](Event对象)

Event对象代表事件的状态,比如事件在其中发生的元素，键盘按键的状态，鼠标的位置，鼠标按钮的状态。  
事件通常与函数结合使用，函数不会在事件发生前被执行！  

### 事件句柄(Event Handlers)

- onabout  
```
  onabout : 事件会在图像加载被中断时发生。
  当用户在图像完成载入之前放弃图像的装载(如单击了stop按钮)时，就会调用该句柄.

  <img src="aaa.gif" onabout = "alert('Error:Loading of the image was aborted')" />
```


- onblur
```
  onblur: 事件会在对象失去焦点时发生。

  upperCase(){
    var x=document.getElementById("fname").value
    document.getElementById("fname").value=x.toUpperCase()
  }

  <input id="fname" onblur={this.upperCase}/>
```


- onchange
```
onchange : 事件会在域的内容改变时发生.

upperCase(x){
    var y=document.getElementById(x).value
    document.getElementById(x).value=y.toUpperCase()
  }

<input type="text" id="fname" onchange="upperCase(this.id)" />
```


- onclick
```
onclick : 事件会在对象被电击时发生。

Field1: <input type="text" id="field1" value="Hello World!">
Field2: <input type="text" id="field2">
点击下面的按钮，把 Field1 的内容拷贝到 Field2 中：
  
<button onclick="document.getElementById('field2').value=document.getElementById('field1').value">Copy Text</button>
```


- ondbclick
```
ondblclick 事件会在对象被双击时发生。

Field1: <input type="text" id="field1" value="Hello World!">
Field2: <input type="text" id="field2">
双击下面的按钮，把 Field1 的内容拷贝到 Field2 中：


<button ondblclick="document.getElementById('field2').value=
document.getElementById('field1').value">Copy Text</button>

```


- onerror
```
onerror : 事件会在文档或图像加载过程中发生错误时被触发。

<img src="aaa.gif" onerror = "alert('The image could not be loaded')" />
```


- onfocus
```
onfocus : 事件在对象获得焦点时发生.

setStyle(x){
  document.getElementById(x).style.backgroud="yellow"
}

<input type="text" onfocus="setStyle(this.id)" id="fname">
```


- onkeydown
```
onkeydown : 事件会在用户 按下一个键盘键时发生.

// 用户无法在输入框中输入数字：

function noNumbers(e){
  var keynum,keychar,numcheck

  if(window.event){
    keynum = e.keyCode
  }else(e.which){
    keynum = e.which
  }

  keychar = String.fromCharCode(keynum)
  numcheck=/\d/
  return !numcheck.test(keychar)

}


<form>
  <input type='text' onkeydown="return noNumbers(event)" />
</form>

```


- onkeypress
```
  onkeypress : 事件会在键盘被按下并释放一个键时发生

  noNumbers(e){
    var keynum
    var keychar
    var numcheck

    if(window.event){
      keynum = e.keyCode
    }eles if(e.which){
      keynum = e.which
    }

    keychar = String.fromCharCode(keynum) 
    numcheck=/\d/
    return !numcheck.test(keychar) 
  }


  <form>
  <input type='text' onkeypress="return noNumbers(event)"/>
  </form>
```


- onkeyup
```
onkeyup 事件会在键盘按键被松开时发生

upperCase(x){
  var y = document.getElementById(x).value = y.toUpperCase()
}

...

<input type="text" id="fname" onkeyup="upperCase(this.id)"/>
```


- onload
```
onload事件会在页面或图像加载完成后立即发生

load(){
  window.status = "Page is loaded"
}

<body onload="load()"></body>
```


- onmousedown
```
onmousedown 事件会在鼠标按键被按下时发生

<img src="asda.gif"  onmousedown="alert('You clicked the picture!')"/>

```


- onmousemove
```
  onmousemove 事件会在鼠标指针移动时发生

<img src="asda.gif"  onmousemove="alert('您的鼠标刚才经过了图片!')"/>

```


- onmouseover
```
onmouseout 事件会在鼠标指针移出指定的对象时发生

<img src="asda.gif"  onmouseover="alert('您的鼠标在图片上!')"/>

```


- onmouseup
```
onmouseup 事件会在鼠标按键被松开时发生

<img src="/i/eg_mouse2.jpg" alt="mouse" onmouseup="alert('您点击了图片！')" />
```


- onreset
```
onreset 事件会在表单中的重置按钮被点开时发生

<form onreset="alert(The form will be reset) ">
  Firstname: <input type="text" name="fname" value="John" />
  Lastname: <input type="text" name="lname" />
  <input type="reset" value="Reset" />
</form>

```


- onresize
```
onresize 事件会在窗口或框架被调整大小时发生

<body onresize="alert('You have changed the size of the window')">

</body>

```


- onsubmit
```
onsubmit 事件会在表单中的确定按钮被电击时发生

<form name="testform" action="jsref_onsubmit.asp"onsubmit="alert('Hello ' + testform.fname.value +'!')">
  
  What is your name?<br />
<input type="text" name="fname" />
<input type="submit" value="Submit" />

</form>
```


- onunload
```
onunload 事件在用户退出页面时发生

<body onunload="alert('The onunload event was triggered')">
</body> 
```


### 鼠标/键盘属性

- altKey
```
altKey 事件属性返回一个布尔值。指示在指定的事件发生时，Alt 键是否被按下并保持住了。

function isKeyPressed(event){
  alert("The ALT key was pressed!")
}else{
  alert("The ALT key was Not pressed!")
}

<body onmousedown="isKeyPressed(event)">

<p>Click somewhere in the document.
An alert box will tell you if you 
pressed the ALT key or not.</p>

</body>
```


- button
```
button事件属性可返回一个整数，指示当事件被触发时哪个鼠标按键被点击。

event.button = 0|1|2

0 规定鼠标左键
1 规定鼠标中键
2 规定鼠标右键

Internet Explorer 拥有不同的参数：

0 规定鼠标左键
4规定鼠标中键
2 规定鼠标右键


function whichButton (event){
  if(event.button === 2){
    alert("You clicked the right mouse button!")
  }else {
    alert("You clicked the left mouse button!")
  }
}

<body onmousedown="whichButton(event)">
<p>Click in the document. An alert box will 
alert which mouse button you clicked.</p>
</body>

```


- clientX
```
clientX事件属性返回当事件被触发时鼠标指针向对于浏览器页面（或客户区）的水平坐标.

客户区指的是当前窗口
  
function show_coords(event){
  x= event.clientX
  y= event.clientY
  alert("X coords: " + x + ",Y coords:" + y)
}  

<body onmousedown="show_coords(event)">
  <p>Click in the document. An alert box will alert 
the x and y coordinates of the mouse pointer.</p>
</body>
```


- clientY
```
clientY 事件属性返回当事件被触发时鼠标指针向对于浏览器页面(客户区)的垂直坐标。

客户区指的是当前窗口


同上
```


- ctrlKey
```
ctrlKey 事件属性可返回一个布尔值，指示当事件发生时，Ctrl 键是否被按下并保持住。

event.ctrlKey = true|false|1|0

function isKeyPressed(event){
  if(event.ctrlKey === 1){
    alert("The CTRL key was pressed!")
  }else {
    alert("The CTRL key was NOT pressed!")
  }
}


<body onmousedown="isKeyPressed(event)">
  
  <p>Click somewhere in the document.
An alert box will tell you if you 
pressed the CTRL key or not.</p>

</body>
```


- metaKey
```
metaKey 事件属性可返回一个布尔值，指示当事件发生时

function isKeyPressed(event){
  if (event.metaKey==1)
  {
  alert("The meta key was pressed!")
  }
else
  {
  alert("The meta key was NOT pressed!")
  }
}


<body onmousedown="isKeyPressed(event)">
  
<p>Click somewhere in the document.
An alert box will tell you if you 
pressed the meta key or not.</p>

</body>
```


- relatedTarget
```
relatedTarget 事件属性返回与事件的目标节点相关的节点

对于 mouseover 事件来说，该属性是鼠标指针移到目标节点上时所离开的那个节点。

对于 mouseout 事件来说。该属性是离开目标时，鼠标指针进入的节点。

对于其他类型的事件来说，这个属性没用.

function getRelElement(event){
  var txt = "The cursor just exited the";
  txt = txt + event.relatedTarget.tagName + "element";
  alert(txt);
}

<p onmouseover="getRelElement(event)"> Mouse over this paragraph</p>

```


- screenX
```
screenX 事件属性可返回事件发生时鼠标指针相对于屏幕的水平坐标.

show_coords(event){
  x=event.screenX
  y=event.screenY
  alert("X coords:" + x +", Y coords:" + y)
}


<p>Click in the document. An alert box will alert 
the x and y coordinates of the cursor.</p>
```


- screenY
```
screenY 事件属性可返回事件发生时鼠标指针相对于屏幕的垂直坐标

同上
```


- shiftKey
```
shiftKey 事件属性可返回一个布尔值，指示当事件发生时，“SHIFT”键是否被按下并保持住

event.shiftKey = true|false|1|0

isKeyPressed(event){
   if (event.shiftKey==1)
    {
    alert("The shift key was pressed!")
    }
  else
    {
    alert("The shift key was NOT pressed!")
    }
}


<body onmousedown="isKeyPressed(event)">
  
<p>Click somewhere in the document.
An alert box will tell you if you 
pressed the shift key or not.</p>

</body>
```

