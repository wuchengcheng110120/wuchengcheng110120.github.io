## [上一页](course137)
##  【第20个代码模型】 集合输出（Iterator迭代输出）

在之前使用集合输出的时候都利用了toString()，或者是利用了List接口中的get()方法，但是这些都不是集合的标准输出模式，如果从标准上来讲，集合的输出一共有四种手段：Iterator、ListIterator、Enumeration、foreach。

95%的集合输出都使用Iterator迭代输出。

在JDK1.5之前Collection接口里面就定义有iterator()方法，通过此方法可以取得Iterator接口的实例化对象，而在JDK1.5之后将此方法提升为了Iterable接口中的方法，但是不管你如何提升，必须清楚只要Collection有这个方法，那么List和Set一定也有此方法。

![](http://ww3.sinaimg.cn/large/0060lm7Tly1foq751a491j30v90hd79v.jpg)

对于Iterator接口最初的设计里面实际上有三个抽象方法：

- 判断是否有下一个元素：public boolean hasNext()

- 取得当前的元素：public E next()

- 删除元素：public default void remove()，此方法从JDK1.8开始变为了default的完整方法

**范例** 标准的Iterator使用：

	package cn.mldn.demo;
	
	import java.util.ArrayList;
	import java.util.Iterator;
	import java.util.List;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			List<String> all = new ArrayList<String>();
			all.add("Hello");
			all.add("Hello");
			all.add("World");
			Iterator<String> iter = all.iterator(); //实例化Iterator接口对象
			while (iter.hasNext()) {
				String str = iter.next();
				System.out.println(str);
			}
		} 	
	}
**console：**

	Hello
	Hello
	World

对于Iterator接口中提供的remove()方法主要解决的就是集合内容中的删除操作（这个真没用）

**范例** 删除元素：

	package cn.mldn.demo;
	
	import java.util.ArrayList;
	import java.util.Iterator;
	import java.util.List;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			List<String> all = new ArrayList<String>();
			all.add("Hello");
			all.add("Hello");
			all.add("a");
			all.add("World");
			Iterator<String> iter = all.iterator(); //实例化Iterator接口对象
			while (iter.hasNext()) {
				String str = iter.next();
				if ("a".equals(str)) { // 要删除的信息
					//all.remove("a"); 如果使用此操作则删除后中断执行
					iter.remove();  //删除后不中断后续执行
					continue;
				}
				System.out.println(str);
			}
		} 	
	}
**console：**

	Hello
	Hello
	World

集合的核心功能在于数据的添加和数据的取出，所以对于删除的操作，在开发中可能使用到的几率是约等于0的。
以后见到了集合输出的问题默认直接使用Iterator。



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course139)
