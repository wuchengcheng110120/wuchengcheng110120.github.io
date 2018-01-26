## [上一页](course94)
##  认识反射机制

反射指的是对象的反向处理操作，首先来观察一下“正”的操作。在默认的情况下必须要先导入一个包，而后才能产生类的实例化对象

**范例** 通过类实例化对象：

	import java.util.Date;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			Date date = new Date(); //正常通过类才能够产生实例化对象
		} 
	}

所谓的反指的是，根据对象取得对象的来源信息，而这个“反”的操作核心的处理就在于Object类的一个方法：

- 取得class对象：public final Class<?> getClass()

该方法返回的是一个class类对象，这个class描述的就是类。

**范例** 调用getClass()

	import java.util.Date;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			Date date = new Date(); //正常通过类才能够产生实例化对象
			System.out.println(date.getClass());
		} 
	}
**console：**

	class java.util.Date

此时通过对象取得了对象的来源，这就是“反”的本质。

反射看重的不再是对象，而是对象身后的组成（类、构造、普通、成员等）。



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course96)
