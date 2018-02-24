## [上一页](course140)
##  【第20个代码模型】 集合输出（foreach输出）

从JDK1.5开始foreach可以输出数组，实际上除了数组之外也可以输出集合操作。不过对于初学者而言不建议这样处理。

**范例** 直接使用foreach进行输出：

	package cn.mldn.demo;
	
	import java.util.ArrayList;
	import java.util.List;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			List<String> all = new ArrayList<String>();
			all.add("Hello");
			all.add("Hello");
			all.add("a");
			all.add("World");
			for(String str : all) {
				System.out.println(str);
			}
			
		} 	
	}
**console：**

	Hello
	Hello
	a
	World

如果从代码的本质上来讲此处是少了一个对象，但是Iterator只是一个输出对象，而所有的内容还是在集合本身，Iterator的一点点空间占用不算什么。

1、看见集合输出使用Iterator即可。

2、Iterator和Enumeration接口中的方法一定要掌握牢固。



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course142)
