# 使用electron 调取camera

```js
	
	navigator.mediaDevices.getUserMedia({ video:true })
	 .then(function(stream){
	 		document.getElementById('camera').src = URL.createObjectURL(stream);
	 }).catch(function(){
	 	  alert('could not commect stream')
	 })

```