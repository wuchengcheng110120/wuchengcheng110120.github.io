## [上一页](course19)
## Annotation（压制警告）

@SuppressWarning

当调用了某些操作可能产生问题的时候就会出先警告信息，但是警告信息并不是错误，在你自己的可控访问里面，会认为警告没有意义，这个时候又不想总提示警告，就可以对警告进行压制。

	package cn.mldn.demo;
	
	class Person<T> {
		@Deprecated 	//表示该方法已经不建议使用了，但是即使使用了也不会出错
		public Person() {}
		public Person(String name) {}
		@Deprecated
		public void fun() {}
	}
	public class TestDemo {
		@SuppressWarnings({ "rawtypes", "unused" })
		public static void main(String[] args) {
			Person per = new Person();//明确的标记出已过期
		}
	}
在Eclipse中出现这些警告，可以通过代码的纠正处理压制警告。

这三种Annotation是JDK默认支持的程序类中使用的，以后会接触一些功能性的Annotation。






## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course21)
