#基础

-[v-show](#v-show)  
-[v-on](#v-on)  

## v-show
 
 控制元素的显示和隐藏


## v-on

我们可以用v-on 指令绑定一个事件监听器，通过它调用我们Vue实例中定义的方法。  

```
<html lang="en">
	<head>
		<meta charset="utf-8">
		<title></title>
		<script src="vue.js"></script>
	</head>
	<body>
		<div id="test">{{msg}}
			<p v-for="val in arr">
				{{ val.a }}
			</p>
			<a href="javascript:void(0)" v-on:click="tap">点我</a>
		</div>
	</body>
</html>

<script>
	window.onload = function(){
		var app2 = new Vue({
			el: "#test",
			data:{
				msg: '232',
				msg1: '555' + new Date(),
				msg2: '666',
				show: true,
				arr:[
					{a: 'bb'},
					{a: 'cc'}
				]
			},
			methods: {
				tap: function(){
					this.arr.unshift({ a: 'new' })
				}
			}
		})
	}
</script>

```