## 2类与对象 ##
### 2.1类与对象（类与对象的基本定义） ###

	class 类名 {
		
		属性；
		属性；
		方法（）{
		    }
			
	}

类定义完之后是不能够直接去使用的，想要使用类那么必须产生对象
	
    而对象的定义分为以下两种语法形式：
 		
	声明并实例化对象： 类名称 对象名称 = new 类名称（）；

	分步进行对象实例化：
		声明对象：类名称 对象名称 = null
		实例化对象：对象名称 = new 类名称

引用数据类型的最大特征在于内存的分配 而只要出现有关键字new，那么就只有一个解释 ：new 开辟内存

内存是不可能无线开辟的，所以这个时候所谓的性能调优调整的就是内存问题