## [上一页](course134)
##  【第19个代码模型】 Set集合接口（Set接口常用子类）

Set接口与List接口最大的不同在于Set接口中的内容是不允许重复的，同时也需要注意一点，Set与List还有一个最大的不同在于：Set接口并没有对Collection接口进行扩充，而List对Collection进行了扩充。由于是JDK1.8的原因所以在Collection接口里面也提供有一些default方法，而这些方法并没有在Set接口出现。也就是说Set接口里面是不可能直接使用get()方法进行处理的，而在Set子接口中有两个常用的子类：HashSet、TreeSet。

![](https://s1.ax1x.com/2018/02/21/9N2GqO.png)

**范例** 观察HashSet的使用：

	package snippet;
	
	import java.util.HashSet;
	import java.util.Set;
	
	public class Snippet {
		public static void main(String[] args) {
			Set<String> all = new HashSet<String>();
			all.add("Hello") ;
			all.add("Hello") ; //重复元素
			all.add("World") ;
			all.add("MLDN") ;
			all.add("ABC") ;
			System.out.println(all);
		}
	}
**console：**

	[ABC, Hello, World, MLDN]

**范例** 观察TreeSet的使用：

	package snippet;
	
	import java.util.Set;
	import java.util.TreeSet;
	
	public class Snippet {
		public static void main(String[] args) {
			Set<String> all = new TreeSet<String>();
			all.add("C") ;
			all.add("C") ; //重复元素
			all.add("A") ;
			all.add("B") ;
			all.add("D") ;
			System.out.println(all);
		}
	}
**console：**

	[A, B, C, D]

TreeSet使用的是升序排列。


## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course136)
