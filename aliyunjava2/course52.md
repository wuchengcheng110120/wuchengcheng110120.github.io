## [上一页](course51)

##  内部类的定义和使用（在方法中定义内部类）


理论上内部类可以定义在类中的任意位置上，这就包括了类中，方法中，以及代码块中，从实用的角度来讲，在方法中定义内部类的形式是最多的。

**范例** 在方法中定义内部类：

	class Outer{
		private String msg  = "Hello World ! ";
		public void fun(int num) {
			class Inner{
				public void print() {
					System.out.println(" msg = " + num);
					System.out.println(" msg = " + msg);
				}
			}
			new Inner().print();//产生了内部类的对象并且调用方法
		}
	}
	
	public class TestDemo {
		public static void main(String args[]) {
			new Outer().fun(100);
		}
	}

此时的代码在JDK1.8是正常的，在JDK1.8之前是错误的（目前使用最多的是JDK1.7的支持而不是JDK1.8）。

在JDK1.7及之前，如果一个内部类定义在方法之中，那么该内部类如果想要访问方法中的参数，那么这个参数前必须使用final定义。而JDK1.8之后为了推广它的函数式编程，所以将这一局限取消了。

内部类的使用暂时不作为程序设计首选，但是至少应该知道内部类具备的特点：

- 破坏了程序的结构

- 方便进行私有属性的访问

	class Outer{
		private String msg  = "Hello World ! ";
		public void fun(int num) {
			class Inner{
				private String info = " mldn";
				public void print() {
					System.out.println(" msg = " + num);
					System.out.println(" msg = " + msg);
				}
			}
			System.out.println(new Inner().info);
			new Inner().print();//产生了内部类的对象并且调用方法
		}
	}
	
	public class TestDemo {
		public static void main(String args[]) {
			new Outer().fun(100);
		}
	}

**console：**

	 mldn
	 msg = 100
	 msg = Hello World ! 

- 以后如果发现类名称上出现了“.”应立刻想到是内部类的概念。

## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course53)
