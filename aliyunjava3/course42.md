## [上一页](course41)
## StringBuffer类

Java类库很多，学会查询文档；

回顾： String类特点：

- 任何字符串常量都是String对象，而且String的常量一旦声明则不可改变，如果改变对象的内容改变的是其引用的指向而已。

虽然在很大程度上来讲，String的使用比较简单，但是String的这种不可更改的切点并不好，所以为了方便字符串的修改专门提供有一个StringBuffer类，而在String类里面使用的是“+”来进行的字符串连接，但是这个操作在StringBuffer类里面需要更换为append()方法：

public StringBuffer append(数据类型 x)

**范例** 观察StrinBuffer的使用：

	public class TestDemo {
		public static void main(String[] args) throws Exception {
			StringBuffer buf = new StringBuffer();//建立一个StringBuffer类的对象
			buf.append("hello ").append(" world !");
			fun(buf);
			System.out.println(buf);
		}
		public static void fun(StringBuffer temp) {
			temp.append("\n").append("www.mldn.cn");
		}
	}

**console：**

	hello  world !
	www.mldn.cn

String与StringBuffer的最大区别在于：String的内容无法修改，StringBuffer的内容允许修改。但是需要清楚一点，在开发中优先选择String类，只有在频繁修改的时候才会使用StringBuffer类。

为了更好的理解String与SringBuffer，那么下面来观察这两个类的继承结构：

String类继承结构：

java.lang.Object
java.lang.String

public final class String extends Object implements Serializable, Comparable<String>, CharSequence

StringBuffer类：

java.lang.Object
java.lang.StringBuffer


public final class StringBuffer extends Object implements Serializable, CharSequence

两个类都是charSequence的接口子类，这个借口描述的是字符集，所以字符串就属于字符集的子类，如果以后看见了charSequence最简单的联想就是个字符串。

	public class TestDemo {
		public static void main(String[] args) throws Exception {
			CharSequence seq = "hello";//字符串， 子类为父接口实例化；
		}
	}

这个时候来观察StringBuffer类的构造方法：

public StringBuffer(CharSequence seq)

但是这个时候有一个小小的问题需要注意：虽然String与StringBuffer都属于CharSequence接口的一个子类，但是这两个类对象不能直接转换。如果想要转换，可以采用如下原则：

- String变为StringBuffer：利用StringBuffer的构造、append()方法；

	package cn.mldn.demo;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			String str = "hello";
			//StringBuffer buf = new StringBuffer(str);
			StringBuffer buf = new StringBuffer();
			buf.append(str);
			System.out.println(buf);
		}
	}

- StringBuffer变为String：所有对象都有一个将对象变为String的方法，使用toString()方法；

实际上StringBuffer还是有一些String类所没有的特点的：

1、 支持字符串反转：

public StringBuffer reverse()

	package cn.mldn.demo;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			StringBuffer buf = new StringBuffer("HelloWorld");
			System.out.println(buf.reverse());
		}
	}
**console：**
	
	dlroWolleH

2、 可以删除指定范围的数据：

public StringBuffer delete(int start,
                           int end)

	package cn.mldn.demo;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			StringBuffer buf = new StringBuffer("HelloWorld");
			System.out.println(buf.delete(5, 10));
		}
	}

**console：**
	
	Hello

3、 在指定位置插入数据：

public StringBuffer insert(int offset,
                           String str)

	package cn.mldn.demo;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			StringBuffer buf = new StringBuffer("HelloWorld");
			System.out.println(buf.delete(5, 10).insert(0, "你好"));
		}
	}

**console：**
	
	你好Hello

请解释String、StringBuffer、StringBuilder的区别？

- String不可修改，StringBuffer和StringBuilder可以修改；

- StringBuffer采用同步处理，属于线程安全操作，而StringBuilder采用异步处理，属于线程不安全操作。

优先考虑String，StringBuffer和StringBuilder只是作为备选方案。


## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course43)
