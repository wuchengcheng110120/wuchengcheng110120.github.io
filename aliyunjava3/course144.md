## [上一页](course143
##  【第21个代码模型】 Map集合（Hashtable子类）

JDK1.0提供有三大主要类：Vector、Enumeration、Hashtable。Hashtable是最早实现这种二元偶对象数据结构的，后期的设计也让其与Vector类一样多实现了Map接口而已。

**范例** 观察Hashtable：

	package cn.mldn.demo;
	
	import java.util.Hashtable;
	import java.util.Map;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			Map<Integer, String> map = new Hashtable<Integer,String>();
			map.put(3, "MLDNJava");
			map.put(1, "Hello");
			map.put(1, "World"); //key重复
			map.put(2, "MLDN");
			System.out.println(map);
		} 	
	}
**console：**

	{3=MLDNJava, 2=MLDN, 1=World}

请解释HashMap与Hashtable的区别？

- HashMap： JDK1.2出现，异步处理性能高，非线程安全，允许存放空

- Hashtable：JDK1.0出现，同步处理性能较低，线程安全，不允许key和value存放空否则出现NullPointerException

HashMap使用的频率更高

![](http://ww3.sinaimg.cn/large/0060lm7Tly1fov4qwoiggj30v20h8tgk.jpg)



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course145)
