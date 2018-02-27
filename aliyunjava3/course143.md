## [上一页](course142)
##  【第21个代码模型】 Map集合（HashMap子类）

HashMap是在使用Map集合里面最为常用的一个子类，下面先通过HashMap进行一个Map的使用操作。

**范例** Map的基本处理：

	package cn.mldn.demo;
	
	import java.util.HashMap;
	import java.util.Map;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			Map<Integer, String> map = new HashMap<Integer,String>();
			map.put(3, "MLDNJava");
			map.put(1, "Hello");
			map.put(1, "World"); //key重复
			map.put(2, "MLDN");
			System.out.println(map);
			System.out.println(map.get(1));  //根据key取值
			System.out.println(map.get(99));  //根据key取值
		} 	
	}
**console：**

	{1=World, 2=MLDN, 3=MLDNJava}
	World
	null

**范例** 取得一个Map中所有key的信息：

	package cn.mldn.demo;
	
	import java.util.HashMap;
	import java.util.Iterator;
	import java.util.Map;
	import java.util.Set;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			Map<Integer, String> map = new HashMap<Integer,String>();
			map.put(3, "MLDNJava");
			map.put(1, "Hello");
			map.put(1, "World"); //key重复
			map.put(2, "MLDN");
			Set<Integer> set = map.keySet(); // 取得所有的Key信息
			Iterator<Integer> iter = set.iterator();
			while (iter.hasNext()) {
				Integer key = iter.next();
				System.out.println(key + " = " + map.get(key));
			}
		} 	
	}
**console:**

	1 = World
	2 = MLDN
	3 = MLDNJava

此种输出操作没有任何实际意义，只是为了对其做一个功能使用的说明，因为这样的输出处理复杂度太高了：N*N，有多少数据就要查询多少次。

请解释HashMap的原理：

在数据量小的时候，HashMap是按照链表的形式存储的。当数据量增大之后，为了快速的查找，那么会将这个链表变为红黑树（均衡二叉树），用hash码作为数据的定位，来进行保存的。


## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course144)
