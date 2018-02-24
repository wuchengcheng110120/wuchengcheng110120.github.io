## [上一页](course139)
##  【第20个代码模型】 集合输出（Enumeration枚举输出）

在JDK1.0的时候就引入了Enumeration的接口，而在JDK1.5时对其进行了更正，主要是追加了泛型的应用，那么首先来观察Enumeration的接口的方法定义：

- 判断是否有下一个元素：public boolean hasMoreElements()

- 取得元素：public E nextElement()

但是想要取得这个接口的实例化对象，是不可能依靠Collection、List、Set等接口的，只能够依靠Vector子类，因为Enumeration最早的设计就是为Vector服务的，在Vector子类中提供有一个取得Enumeration接口对象的方法：

- 取得Enumeration的接口对象：public Enumeration<E> elements()

**范例** Enumeration使用：

	package cn.mldn.demo;
	
	import java.util.Enumeration;
	import java.util.Vector;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			Vector<String> all = new Vector<String>();
			all.add("Hello");
			all.add("Hello");
			all.add("a");
			all.add("World");
			Enumeration<String> enu = all.elements();
			while (enu.hasMoreElements()) {
				System.out.println(enu.nextElement());
			}
			
		} 	
	}
**console：**

	Hello
	Hello
	a
	World

一些操作类库上依然只支持Enumeration，而不支持Iterator，虽然很少，但在开发中可能会遇到。


## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course141)
