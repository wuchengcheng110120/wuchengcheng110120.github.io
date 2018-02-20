## [上一页](course133)
##  【第18个代码模型】 List集合接口（LinkedList子类）

在List接口里面还有一个LinkedList子类，这个子类如果向父接口转型的话，使用和之前没有任何的区别。

	package cn.mldn.demo;
	import java.util.LinkedList;
	import java.util.List;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			List<String> all = new LinkedList<String>();
			all.add("Hello") ;
			all.add("Hello") ; //重复数据
			all.add("World") ;
			all.remove("Hello");
			System.out.println(all);
		} 	
	}

面试题：请解释ArrayList和LinkedList的区别？

1、 首先来观察ArrayList的核心代码：可以发现ArrayList中存的是一个对象数组，如果在实例化此类对象的时候我们默认传入了数组的大小，则保存的数组里面就会开辟一个定长的数组，但是如果在后面数据保存的时候发现数组的个数不够了，那么会进行数组的动态扩充。所以很明显在实际的开发之中使用ArrayList的最好的做法就是设置初始化的大小（以分页的程序为例，每次只会取出指定行的内容），避免频繁扩充，提升性能。

构造方法：

	public ArrayList() {
	    this.elementData = DEFAULTCAPACITY_EMPTY_ELEMENTDATA;
	}

常量：

 	private static final Object[] DEFAULTCAPACITY_EMPTY_ELEMENTDATA = {};

2、 LinkedList： 是一个纯粹的链表实现，与之前编写的链表程序的实现完全一样（比自编的性能好）

总结：ArrayList封装的是一个数组， LinkedList封装的是一个链表实现，ArrayList的时间复杂度为1（适合随机访问，读取），而LinkedList的时间复杂度为n（适合增删）。

开发之中使用ArrayList使用更多，考虑性能就初始化大小。



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course135)
