## [上一页](course48)

##  代码块（静态代码块）

静态块指的是使用static关键字定义的代码块。但是如果要考虑静态块必须要考虑两种情况：

- 是在非主类中定义的静态块；

- 在主类中定义的静态块；


**范例** 观察静态块定义：

	class Person{
	
		{
			System.out.println("1 、 Person类的构造块" );
		}
		public Person(){
			System.out.println("2 、 Person类的构造方法");
		}
		static{//静态块
			System.out.println("3 、 Person类的静态块");
		}
	}
	
	public class TestDemo {
		public static void main(String args[]) {
			new Person();
			new Person();
		}
	}

**console：**
	
	3 、 Person类的静态块
	1 、 Person类的构造块
	2 、 Person类的构造方法
	1 、 Person类的构造块
	2 、 Person类的构造方法

可以发现静态块优先于构造块执行，不管产生多少个实例化对象，静态块也只使用一次。静态块最为主要的作用就是为static属性进行初始化。

	class Person{
		private static String info = "hello";
		{
			System.out.println("1 、 Person类的构造块" );
		}
		public Person(){
			System.out.println("2 、 Person类的构造方法");
		}
		static{//静态块
			info  += " world !!!";//对static进行初始化配置
			System.out.println("3 、 Person类的静态块" + info);
		}
	}
	
	public class TestDemo {
		public static void main(String args[]) {
			new Person();
			new Person();
		}
	}

**console：**

	3 、 Person类的静态块hello world !!!
	1 、 Person类的构造块
	2 、 Person类的构造方法
	1 、 Person类的构造块
	2 、 Person类的构造方法

静态块也可以定义在主类中，那么静态块将优先于主方法执行。

	public class TestDemo {
		static {
			System.out.println("*******************");
		}
		public static void main(String args[]) {
			System.out.println("Hello World !");
		}
	}

**console：**

	*******************
	Hello World !

如果对于一些属性在使用前进行处理，就可以使用构造块或静态块完成。同步代码块将在多线程时学习。


## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course50)
