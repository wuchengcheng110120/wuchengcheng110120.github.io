## [上一页](course145)
##  【第21个代码模型】 Map集合（Map使用Iterator输出）

在实际的开发过程中，如果储存数据是为了输出，那么优先考虑的一定是Collection，使用Map的主要操作就是设置内容，而后通过get()进行查找的。使用Map迭代输出的需求会有，但是不多。如果想要观察输出首先必须明确一点：Map接口没有iterator()方法。下面通过一个简单的图形来观察Collection与Map保存数据的区别。

![](http://ww4.sinaimg.cn/large/0060lm7Tly1foxgwv6d32j30vc0hhtde.jpg)

在Map接口里面有一个重要的方法，将Map集合转为Set集合：

-  public Set<Map.Entry<K,V>> entrySet()

![](http://ww2.sinaimg.cn/large/0060lm7Tly1foxh5ms0nkj30vb0hfwke.jpg)

**范例** 通过Iterator输出Map集合：

	package cn.mldn.demo;
	
	import java.util.HashMap;
	import java.util.Iterator;
	import java.util.Map;
	import java.util.Set;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			Map<Integer, String> map = new HashMap<Integer,String>();
			map.put(1, "Hello");
			map.put(2, "World");
			Set<Map.Entry<Integer, String>> set = map.entrySet();// 1、将Map集合变为Set集合：
			Iterator<Map.Entry<Integer, String>> iter = set.iterator(); // 2、实例化iterator接口
			while (iter.hasNext()) { // 3、迭代输出取出每一个Map.Entry对象
				Map.Entry<Integer, String> me = iter.next();   // 4、取出Map.Entry
				System.out.println(me.getKey() + " = " + me.getValue());  // 5、取得key和value
			}
		} 	
	}
**console：**

	1 = Hello
	2 = World

以上的形式相比较Collection（List、Set）而言出现的几率不高，但是依然需要熟练使用。



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course147)
