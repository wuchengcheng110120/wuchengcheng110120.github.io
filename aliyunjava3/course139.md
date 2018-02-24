## [上一页](course138)
##  【第20个代码模型】 集合输出（ListIterator双向迭代）

Iterator输出接口有一个缺点，只能够由前向后进行内容的迭代处理，而如果想要进行双向迭代，那么就必须依靠Iterator的子接口：ListIterator来实现，首先来观察一下此接口定义的方法：

- 判断是否有上一个元素：public boolean hasPrevious()

- 取得当前元素：public E previous()

Iterator接口的对象是由Collection接口支持的，但是ListIterator是由List接口支持的，List接口提供有如下方法：

- 取得ListIterator接口对象： public ListIterator<E> listIterator()

![](http://ww2.sinaimg.cn/large/0060lm7Tly1forn17wdmlj30vh0he7bm.jpg)

**范例** ListIterator双向迭代输出
	
	package cn.mldn.demo;
	
	import java.util.ArrayList;
	import java.util.List;
	import java.util.ListIterator;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			List<String> all = new ArrayList<String>();
			all.add("Hello");
			all.add("Hello");
			all.add("a");
			all.add("World");
			ListIterator<String> iter = all.listIterator();
			System.out.println("由前向后输出：" );
			while (iter.hasNext()) {
				System.out.print(iter.next() + "、");
			}
			System.out.println("\n由后向前输出：" );
			while (iter.hasPrevious()) {
				System.out.print(iter.previous() + "、");
			}
		} 	
	}
**console：**

	由前向后输出：
	Hello、Hello、a、World、
	由后向前输出：
	World、a、Hello、Hello、

如果想要由后向前输出，那么应该首先实现由前向后的输出否则无法实现双向



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course140)
