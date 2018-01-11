## [上一页](course44)
## System类

之前使用的System.out.println()，实际上之前学习过的数组拷贝就属于System类中的一个方法.

java.lang.Object
java.lang.System

public final class System
extends Object

数组拷贝：

	public static void arraycopy(Object src,
                             int srcPos,
                             Object dest,
                             int destPos,
                             int length)

在这个类中有一个取得日期时间数的方法：

- public static long currentTimeMillis()

此方法可以取得某个操作所需的时间：

	package cn.mldn.demo;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			long start =System.currentTimeMillis();
			String str = "";
			for (int i = 0; i < 9222; i++) {
				str +=i;
			}
			long end = System.currentTimeMillis();
			System.out.println("花费时间" + (end - start));
		}
	}
**console：**

	花费时间189

- public static void gc()，也提供有一个垃圾收集方法：

		public static void gc() {
		        Runtime.getRuntime().gc();
		    }
		public native void gc();

调用Runtime中的gc()方法，由JVM去实现。

之前强调： 一个类对象的创建一定要使用构造方法，那么一个对象如果不使用了，就应该被释放，那么被释放的时候应该也有一个方法支持才对。所以此时如果想要做这种收尾的操作，可以让一个类去覆写Object类中的finalize()方法，此方法定义如下：

protected void finalize()
                 throws Throwable


Throwable中包含error

无论在finalize中是否出现异常或者错误，结果不会改变，并且也不会导致程序出错。

**范例** 来观察finalize的使用：

	package cn.mldn.demo;
	
	class Person {
		public Person() {
			System.out.println("哇哇哇， 出来了！");
		}
		@Override
		protected void finalize() throws Throwable {
			System.out.println("我要下地狱了，下辈子不当人了！");
			throw new Exception("我还要再活五百年");
		}
	}
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			Person per =  new Person();
			per = null;
			System.gc();
			System.out.println("冲冲转世不为人了！");
		}
	}

**console：**

	哇哇哇， 出来了！
	冲冲转世不为人了！
	我要下地狱了，下辈子不当人了！

请解释final、finally、finalize()的区别?

- final 是一个关键字，用于定义不能够倍继承的父类、不能够被覆写的方法、常量；

- finally 是异常处理的统一出口；

- finalize（）是Object类中的一个方法，用于在对象回收前进行调用；



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course45)
