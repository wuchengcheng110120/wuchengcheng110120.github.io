## [上一页](course132)
##  【第18个代码模型】 List集合接口（Vector子类）

很少使用。

Vector这个类是从JDK1.0的时候提出的，而ArrayList是在JDK1.2的时候提出的。最初Java在开发类集的时候，曾经考虑取消Vector类，因为这个类的实现机制太古老了，可是后来又考虑已经有很多人习惯使用Vector，于是对Vector进行了重新的设计，让其多实现了一个List接口。

**范例** 使用Vector

	public class TestDemo {
		public static void main(String[] args) throws Exception {
			List<String> all = new Vector<String>();
			all.add("Hello") ;
			all.add("Hello") ; //重复数据
			all.add("World") ;
			all.remove("Hello");
			System.out.println(all);
		} 	
	}

面试题：请解释ArrayList和Vector的区别？

1、 ArrayList JDK1.2才有的，VectorJDK1.0

2、 ArrayList 异步处理性能更好，Vector同步处理

3、 ArrayList 非线程安全， Vector线程安全

4、 ArrayList 支持Iterator、ListIterator、foreach输出，Vector支持支持Iterator、ListIterator、foreach、Enumeration输出

在以后的使用中优先考虑ArrayList。

![](https://s1.ax1x.com/2018/02/20/9N3HOK.png)




## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course134)
