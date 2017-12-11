## [上一页](course50)

##  内部类的定义和使用（static定义内部类）

内部类中如果使用static进行定义，那么就表示其就是一个外部类的形式，但是这个外部类的名称就是“外部类.内部类”，同时该内部类只允许访问外部类中的static操作。

**范例** 使用static定义内部类：

	class Outer{
		private static String msg  = "Hello World ! ";
		static class Inner {// 内部类 = 外部类
			public void print() {
				//此时只能够使用外部类中的static操作
				System.out.println(msg);
			}
		}
	}

那么如果想要操作这个外部类，就要使用如下的语法：

- 实例化对象：外部类.内部类 内部类对象 = new 外部类.内部类（）；

	class Outer{
		private static String msg  = "Hello World ! ";
		static class Inner {// 内部类 = 外部类
			public void print() {
				//此时只能够使用外部类中的static操作
				System.out.println(msg);
			}
		}
	}
	
	public class TestDemo {
		public static void main(String args[]) {
			Outer.Inner in = new Outer.Inner();
			in.print();
		}
	}

以后开发之中一定会见到这样类似的概念，但是很少使用，了解即可。
	

## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course52)
