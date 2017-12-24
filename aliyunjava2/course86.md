## [上一页](course85)

## 单例设计模式（单例设计模式）

所谓的单例设计指的是一个类只允许产生一个实例化对象。下面首先来观察一个简单的程序：

**范例** 观察一个简单的程序：

	class Singleton {
		public void print() {
			System.out.println("Hello World !");
		}
	}
	public class TestSingleton{
		public static void main (String args[]) {
			Singleton s = null; // 声明对象
			s = new Singleton();//实例化对象
			s.print();
		}
	}

以上的程序在实例化Singleton对象的时候调用了Singleton类的无参构造方法，因为在Singleton类里面并没有提供任何构造，所以会自动生成一个无参的什么都不做的构造方法。但是如果说现在将Singleton类中明确定义一个私有参数的构造方法呢？

	class Singleton {
		private Singleton() {}//所有的方法上都可以使用四个权限
		public void print() {
			System.out.println("Hello World !");
		}
	}

这个时候类中提供了一个私有的构造方法，那么默认的无参的构造方法将一定不会自动生成，那么也就是说，此时在进行对象实例化的时候一定会有错误。

首先一旦构造方法被私有化了，那么就表示外部无法调用构造了，也就证明外部不能够产生新的实例化对象了。那么也就证明此时的类是一个相对而言封闭的状态了。

1、 可是现在如果还想调用Singleton类中的print（）这个普通方法，就必须提供有实例化对象。于是根据封装的特点，可以考虑在类的内部产生一个实例化对象。

	class Singleton {
		Singleton instance = new Singleton();//内部产生实例化对象
		private Singleton() {}//所有的方法上都可以使用四个权限
		public void print() {
			System.out.println("Hello World !");
		}
	}

2、 现在Singleton类内部的instance对象（属性）是一个普通属性，所有的普通属性必须在有实例化对象的时候才能够进行内存空间的分配，而现在外部无法产生实例化对象，所以就必须想一个办法，可以在Singleton类没有实例化对象产生的时候也可以讲instance进行使用。那么自然会联想到使用static关键字。

	class Singleton {
		static Singleton instance = new Singleton();//内部产生实例化对象
		private Singleton() {}//所有的方法上都可以使用四个权限
		public void print() {
			System.out.println("Hello World !");
		}
	}
	public class TestSingleton{
		public static void main (String args[]) {
			Singleton s = null;
			s = Singleton.instance;	
			s.print();
		}
	}

3、 以上虽然可以取得了Singleton类中的实例化对象，但是对于类中的属性应该使用private进行封装，而如果想要取得封装的属性就必须提供有一个getter（）方法，不过此时访问的是一个static属性，并且这个类无法在外部进行实例化对象的创建，所以应该再提供有一个static的方法，因为static方法也不受实例化对象的控制。

	class Singleton {
		private static Singleton instance = new Singleton();//内部产生实例化对象
		public static Singleton getInstance() {
			return instance;
		}
		private Singleton() {}//所有的方法上都可以使用四个权限
		public void print() {
			System.out.println("Hello World !");
		}
	}
	public class TestSingleton{
		public static void main (String args[]) {
			Singleton s = null;
			s = Singleton.getInstance();	
			s.print();
		}
	}

首先现在的问题已经解决了，但是这样做法的目的是什么呢？只希望类中产生唯一的一个实例化对象。

不过对于单例设计模式，也有两类形式：懒汉式。饿汉式。之前的程序就属于饿汉式的应用，因为不管你是否去使用Singleton类的一个对象，只要该类加载了，那么一定会创建好一个公共的instance对象。既然是饿汉式就希望整体的操作中就只有一个实例化对象，所以一般还会为其追加上final关键字。

**范例** 饿汉式单例设计：

	class Singleton {
		private final static Singleton INSTANCE = new Singleton();//内部产生实例化对象
		public static Singleton getInstance() {
			return INSTANCE;
		}
		private Singleton() {}//所有的方法上都可以使用四个权限
		public void print() {
			System.out.println("Hello World !");
		}
	}
	public class TestSingleton{
		public static void main (String args[]) {
			Singleton s = null;
			s = Singleton.getInstance();	
			s.print();
		}
	}

例题： 请编写一个Singleton程序，并说明程序的主要特点

- 代码在上面；

- 特点：构造方法私有化，外部无法产生新的实例化对象，只能够通过新的static方法取得实例化对象。

**范例** 懒汉式单例设计：

- 指的是当第一次去使用Singleton类对象的时候才会为其进行实例化的处理操作；

	class Singleton {
		private  static Singleton instance ;//内部产生实例化对象
		public static Singleton getInstance() {
			if (instance == null) {
				instance = new Singleton();
			}
			return instance;
		}
		private Singleton() {}//所有的方法上都可以使用四个权限
		public void print() {
			System.out.println("Hello World !");
		}
	}
	public class TestSingleton{
		public static void main (String args[]) {
			Singleton s = null;
			s = Singleton.getInstance();	
			s.print();
		}
	}

对于饿汉式和懒汉式理解即可，更多的情况是需要将单例设计的核心组成记住以及慢慢理解它的用法。





## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course87)
