# scrollWidth,clientWidth,offsetWidth 的区别

- scrollWidth: 对象的实际内容，不包边线宽度，会随对象中内容超过可视区后而变大。  
- clientWidth: 对象内容的可视区的宽度，不包滚动条等边线，会随对象显示大小的变化而变化。  
- offsetWidth: 对象整体的实际宽度，包括滚动条等边线，会随对象显示大小的变化而变化。  

情况1:  
元素内无内容或者内容不超过可视区，滚动不出现或不可用的情况。  
srcollWidth = clientWidth,两者皆为内容可视区的宽度。  
offsetWidth为元素的实际宽度。   

![图一](../image/对象宽度/p1.jpeg)

情况2:  
元素的内容超过可视区，滚动条出现和可用的情况下。  
scrollWidth>clientWidth.  
scrollWidth为实际内容的宽度。  
clientWidth时内容可视区的宽度。  
offsetWidth时元素的实际宽度.  

![图二](../image/对象宽度/p2.jpeg)
