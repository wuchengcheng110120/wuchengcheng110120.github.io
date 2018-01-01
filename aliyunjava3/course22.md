## [上一页](course21)
## Lambda表达式

Lambda是从JKD1.8开始的重要特性，很多编程语言都开始支持函数式编程，其中最具备代表性的就是haskell。

面向对象和函数式编程，很多人觉得面向对象的概念过于完整，结构操作不明确。

**范例** 传统面向对象开发：

		package cn.mldn.demo;
		
		interface IMessage{
			public void print();//这是一个接口，接口中的抽象方法必须有子类
		}
		public class TestDemo {
			public static void main(String[] args) {
				IMessage msg = new IMessage() {		
					@Override
					public void print() {
						System.out.println("hello world ! ");
					}
				};
				msg.print();
			}
		}
**console：**

	hello world ! 
	
使用匿名内部类来实现接口最大的优点是节约了一个文件，最大的缺点是结构不清晰。于是对于此类操作有了更简化的实现，如果采用的是函数式编程模型：

	package cn.mldn.demo;
	
	interface IMessage{
		public void print();//这是一个接口，接口中的抽象方法必须有子类
	}
	public class TestDemo {
		public static void main(String[] args) {
			// 函数式编程的使用，目的还是输出一句话
			IMessage msg = ()->System.out.println("hello world !");
		}
	}

面向对象的语法最大的局限要求在于：结构必须非常完整。

但是如果想要使用函数式编程有一个前提：接口必须只有一个方法。如果有两个方法那么将无法使用函数。
如果现在某一个接口就是为了函数式编程而生的，最好定义的时候就让其只能够定义一个方法，所以有了一个新的注解：@FunctionInterface

	package cn.mldn.demo;
	
	@FunctionalInterface //是一个函数式编程的接口，只允许有一个方法
	interface IMessage{
		public void print();//这是一个接口，接口中的抽象方法必须有子类
	}
	public class TestDemo {
		public static void main(String[] args) {
			// 函数式编程的使用，目的还是输出一句话
			IMessage msg = ()->System.out.println("hello world !");
			msg.print();
		}
	}

实际上对于以上的语法形式：

- （）-> 单行语句；

![](http://ww4.sinaimg.cn/large/0060lm7Tly1fn13wdzfxpj30vm0hbai5.jpg)

这个时候方法本身只包含一行语句，那么直接编写语句即可，如果要是有多行语句，则就需要使用“{}”。

	package cn.mldn.demo;
	
	@FunctionalInterface //是一个函数式编程的接口，只允许有一个方法
	interface IMessage{
		public void print();//这是一个接口，接口中的抽象方法必须有子类
	}
	public class TestDemo {
		public static void main(String[] args) {
			// 函数式编程的使用，目的还是输出一句话
			IMessage msg = ()->{
				System.out.println("hello world !");
				System.out.println("hello world !");
				System.out.println("hello world !");
			};
			msg.print();
		}
	}

如果现在只是一行返回，就直接使用语句即可：

	package cn.mldn.demo;
	
	@FunctionalInterface //是一个函数式编程的接口，只允许有一个方法
	interface IMath{
		public int add(int x,int y);//这是一个接口，接口中的抽象方法必须有子类
	}
	public class TestDemo {
		public static void main(String[] args) {
			// 函数式编程的使用，目的还是输出一句话
			IMath math = (p1,p2)->	p1+ p2;
			System.out.println(math.add(10, 20));
		}
	}

如果习惯使用函数式编程可以使用Lambda表达式，有一种基于Java的函数式编程语言：Scala。

## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course23)
