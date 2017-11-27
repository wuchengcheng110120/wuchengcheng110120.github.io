## [上一页](course22)

## 7.4 String类的基本特点（String两种实例化的区别）

### 第一种  采用直接赋值：

	String str = "hello";

![](https://i.imgur.com/Cfy9tmp.png)


**范例** 同样的模式进行新的字符串的创建：

	public class StringDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			String str1 = "hello";
			String str2 = "hello";
			String str3 = "hello";
			
			System.out.println(str1 == str2);
			System.out.println(str1 == str3);
			System.out.println(str2 == str3);
		}
	}

**console： **

	true
	true
	true

![](https://i.imgur.com/ZyNpZoS.png)

通过运行结果分析出的内存关系，但是从另外一个方面来讲，为什么并没有开辟新的内存空间？

> String类的设计使用了一个共享设计模式

在JVM的底层实际上会自动维护一个对象池（字符串对象池），现在采用直接的赋值模式进行String类对象的实例化操作，该实例化对象（字符串）将自动的保存到这个对象池之中，如果下次继续使用直接复制的模式声明String类的对象，如果此时对象池之中有指定的内容将直接进行引用，如果没有将开辟新的字符串对象，将其保存在对象池之中，以供下次使用（所谓的对象池就是一个对象数组）。

>缓存？



**范例** 与字符串常量进行比较：

	public class StringDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			String str = "hello";
	
			System.out.println("hello" == str);
			System.out.println("hello" == "hello");
		}
	}


**console： **

	true
	true

一方面与共享设计有关，另一方面与JDK版本有关。

### 第二种 构造方法

采用构造方法进行实例化才属于标准做法

	String str = new String("hello");

![](https://i.imgur.com/BLEi3ZF.png)

通过分析确认，使用构造方法将开辟两块堆内存空间，其中一块堆内存空间将成为垃圾空间，出了这一缺点之外，实际上也会对字符串共享产生问题。

**范例** 观察字符串共享：

	public class StringDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			String str1 = new String("hello");
			String str2 = "hello";
	
			System.out.println(str1 == str2);
		}
	}

**console： **

	false

该字符串常量没有保存在共享池之中，并不表示不能够进入对象池保存：需要手工处理，在String类中一个方法可以自动实现入池操作public String intern（）

**范例** 观察字符串共享：

	public class StringDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			String str1 = new String("hello").intern();
			String str2 = "hello";
	
			System.out.println(str1 == str2);
		}
	}

**console： **

	true

![](https://i.imgur.com/tTyupnw.png)

面试题：请解释String类中两种实例化的区别

- 直接赋值：只会开辟一块堆内存空间，并且该字符串对象可以保存在对象池中以供下次使用；

- 构造方法：会开辟两块堆内存空间，一块将成为垃圾空间，并且不会自动保存在对象池之中，可以使用intern（）方法手工入池。

使用时一般直接赋值String。

## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course24)
