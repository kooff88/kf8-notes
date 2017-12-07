# DOM

## 文档对象模型 (DOM)  
  将web页连接到脚本或编程语言。 通常这意味着javascript,但将HTML,SVG或XML文档建模为对象不是javascript语言的一部分。  
  它给文档（结构树）提供了一个结构化的表述并且定义了一种方式-程序可以对结构树进行访问，以改变文档的结构，样式和内容。  
  DOM提供了一种表述形式-将文档作为一个结构化的节点组以及包含属性和方法的对象。从本质上说，它将web页面和脚本或编程语言  
  连接起来了。  

  尽管通常会使用JavaScript来访问DOM,但它并不是JavaScript的一部分，它也可以被其他语言使用。  

  所有操作和创建web页面的属性，方法和事件都会被组织成对象的形式（例如，document对象表示文档本身，table对象实现了特定的  
  HTMLTableElement DOM接口来访问HTML表格等）。下面介绍基于Gecko浏览器的DOM面向对象引用。  
    ps: Gecko是套开放源代码的，以C++编写的网页排版引擎。使用的浏览器有Netscape 6以后版本、Mozilla Firefox等.  



## DOM和JavaScript

  DOM并不是一个编程语言，但如果没有DOM,JavaScript语言也不会有任何网页，XML页面以及涉及到的元素的概念或模型。  
  在文档中的每个元素-包括整个文档，文档头部，文档中表格，表头，表格中的文本-都是文档所属于的文档对象模型（DOM）的一部分，  
  因此它们和一个脚本语言如JavaScript,来访问和处理。  

  开始的时候，JavaScript和DOM是交织在一起的，但它们最终演变成了两个独立的实体。  
  JavaScript可以访问和操作存储在DOM中的内容，因此我们可以写成这个近似的等式：  

>> API(web或 XML页面) = DOM + JS(脚本语言)  

  DOM被设计成与特定编程语言相独立，使用文档的结构化表述可以通过单一，一致的API获得。  
  尽管我们在本参考文档中会专注于使用JacaScript,但DOM也可以使用其他的语言来实现，以Python为例，代码如下：  

```
  # Python DOM example
  import xml.dom.minidom as m
  doc = m.parse("C:\\Projects||Py\\chap1.sml");
  doc.nodeName # DOM property of document object;
  p_list = doc.getElementsByTagName('para');

```

