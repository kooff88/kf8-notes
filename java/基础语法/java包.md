# Java包

包主要用来对类和接口进行分类。当开发Java程序时，可能编写成百上千的类，因此很有必要对类和接口进行分类。  

包是类的一种文件组织和管理方式，是一组功能相似或相关的类或接口的集合。  
Java package提供了访问权限和命名的管理机制。  

## 包的作用
1. 把功能相似或相关的类或接口组织在同一个包中，方便类的查找和使用。  
2. 如同文件夹一样，包也采用了树形目录的存储方式。同一个包中的类名字是不同的，不同的包的类的名字可以  
   是相同的，当同时调用两个不同包中相同类名的类时，应该加上包名加以区别。因此，包可以避免名字冲突。  
3. 包也限定了访问权限，拥有包访问权限的类才能访问某个类的包。 

## 包的定义 

在一个.java文件中可以一个public类和多个非public类，如果要将这些类组织在一个包当中，则在.java文件中  
除注释以外的第一行使用关键字package即可实现。当需要调用此包中的类时，就可以使用关键字import 进行导入。  
在定义包的时候，应该注意几点：  
1. 为了尽量使包名保持唯一性，包名通常采用小写，按倒写互联网址的形式进行定义。  
   如:com.hank.www表示包文件放置的文件路径为com/hank/www。  
2. 在进行命名包时，应该避免使用与系统发生冲入的名字，如java.lang , java.swing等。  


## java包创建和使用步骤

。。。  

例子:  

在 animals包中加入一个接口(interface)：  

```
	// 文件名： Animal.java
	package animals;

	interface Animal {
		public void eat();
		public void travel();
	}
```


接下来，在同一个包中加入该接口的实现：  

```
	package animals;
	// 文件名： MammalInt.java

	public class MammalInt implements Animal {
		public void eat() {
			System.out.println("Mammal eats");
		}


		public void travel() {
			System.out.println("Mammal travels");
		}

		public int noOfLegs() {
			return 0;
		}

		public static void main (String args[]) {
			MammalInt m = new MammalInt();
			m.eat();
			m.travel();
		}
	}

```
