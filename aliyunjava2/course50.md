## [上一页](course49)

##  内部类的定义和使用（内部类基本概念）

内部类不作为首要的设计原则。


所谓的内部类指的就是一个类的内部进行其他类结构嵌套的操作语法形式。

**范例** 内部类的基本使用：

	class Outer{
		private String msg  = "Hello World ! ";
		//******************************************
		class Inner{//此时定义了一个内部类
			public void print() {//定义一个普通方法
				System.out.println(msg);//调用msg属性
			}
		}
		//******************************************
		//在外部类中定义一个方法，这个方法负责产生内部类对象并且调用print（）方法
		public void fun() {
			Inner in = new Inner();
			in.print();
		}
	}
	
	public class TestDemo {
		public static void main(String args[]) {
			Outer out = new Outer();//外部类对象
			out.fun();//调用了外部类的方法
		}
	}

**console：**

	Hello World ! 

通过以上的代码发现一个问题：程序的结构有些混乱。虽然内部类破坏了程序的结构，从另外的角度来讲，内部类的优势在于外部类的私有访问。

**范例** 将以上程序中的内部类提取到外部，要求实现同样的功能：

- Outer类和Inner类是两个独立的类，Inner类需要访问Outer类中的msg属性，但是Outer类中的msg属性使用了private进行封装，所以封装的属性要被外部访问，那么需要写getter（）方法；

- 在Inner类中的print（）方法如果想要访问msg的内容只能通过getMsg（）方法完成，但是getMsg（）是一个普通方法，必须通过Outer类对象才可以访问，那么这个时候需要把在主方法中的Outer类对象传递到Inner类中。

		class Outer{
			private String msg  = "Hello World ! ";
			//在外部类中定义一个方法，这个方法负责产生内部类对象并且调用print（）方法
			public String getMsg() {//通过此方法才可以取得msg的内容
				return this.msg;
			}
			public void fun() {//3 、 现在由out对象调用了fun（）方法
				Inner in = new Inner(this);//4 、 this 表示当前调用对象
				in.print();//7、 调用方法
			}
		}
		
		class Inner{//此时定义了一个内部类
			private Outer out;
			public Inner(Outer out) {//5、 Inner.out = main.out
				this.out = out;//6、 引用传递
			}
			public void print() {//8、 执行此方法
				System.out.println(this.out.getMsg());//调用msg属性
			}
		}
		public class OuterDemo {
		
			public static void main(String[] args) {
				// TODO Auto-generated method stub
				Outer out = new Outer();//1、 实例化Outer类对象
				out.fun();//2 、 调用了Outer类的方法
			}
		
		}

折腾了半天的目的就是要访问外部类中的private属性。

对于内部类的操作远远不止如此。

1、 通过以上代码可以发现，当前的内部类的访问必须通过外部类的方法才可以完成，如果现在不想通过外部类访问进行调用，想在程序外部调用，那么就必须按照如下的形式进行内部类的实例化对象创建；

- 语法： 外部类.内部类 内部类对象 = new 外部类（）.new 内部类（）

	class Outer{
		private String msg  = "Hello World ! ";
		//******************************************
		class Inner{//此时定义了一个内部类
			public void print() {//定义一个普通方法
				System.out.println(msg);//调用msg属性
			}
		}
		//******************************************
	}
	
	public class TestDemo {
		public static void main(String args[]) {
			Outer.Inner out = new Outer().new Inner();//声明内部类对象
			out.print();
		}
	}
 
之所以要先进行外部类对象实例化，主要的问题在于此时的外部类中存在有属性，这些属性只有开辟实例化对象之后才能够被访问。

2、 如果说现在一个内部类只想被外部类使用，即：不希望直接产生内部类的实例化对象，那么可以使用private定义

	class Outer{
		private String msg  = "Hello World ! ";
		//******************************************
		private class Inner{//此时定义了一个内部类
			public void print() {//定义一个普通方法
				System.out.println(msg);//调用msg属性
			}
		}
		//******************************************
		public void fun() {
			Inner in = new Inner();
			in.print();
		}
	}
	
	public class TestDemo {
		public static void main(String args[]) {
			new Outer().fun();
		}
	}

3、 在进行属性访问的时候都需要习惯性的加上this，所以如果要想在内部类中明确的使用this，那么语法形式应该变成：“外部类.this.属性”，这就表示外部类当前对象的属性
		
	class Outer{
		private String msg  = "Hello World ! ";
		//******************************************
		private class Inner{//此时定义了一个内部类
			public void print() {//定义一个普通方法
				System.out.println(Outer.this.msg);//调用msg属性
			}
		}
		//******************************************
		public void fun() {
			Inner in = new Inner();
			in.print();
		}
	}
	
	public class TestDemo {
		public static void main(String args[]) {
			new Outer().fun();
		}
	}

## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course51)
