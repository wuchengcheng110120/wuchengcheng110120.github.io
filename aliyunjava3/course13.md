## [上一页](course12)
## 枚举（多例与枚举）

枚举是几乎所有编程语言都支持的数据类型，而在Java诞生了十多年后才追加了枚举，所以得出一个结论：从事Java开发可以不会枚举。

回顾多例设计模式，多例模式的特点：构造方法私有化，而类内部需要提供有若干个实例化对象，后面通过static方法返回。

**范例** 定义一个描述颜色基色的多例设计类

	class Color {
		private static final Color RED = new Color("RED");
		private static final Color GREEN = new Color("GREEN");
		private static final Color BLUE = new Color("BLUE");
		private String title;
		private Color(String title) {
			this.title =title;
		}
		public static Color getInstance(int ch) {
			switch (ch) {
				case 0: return RED;
				case 1: return GREEN;
				case 2: return BLUE;
				default:
					return null;
			}
		}
	}
	
	public class TestDemo {
		public static void main(String[] args) {
			System.out.println(Color.getInstance(0));
		}
	}

以上的做法是在JDK1.5之前的做法，这样做的目的是限制本类实例化对象的产生个数。但是从JDK1.5之后有了枚举，代码开发变得简单了：

**范例** 基于枚举开发：

	package cn.mldn.demo;
	
	enum Color {
		RED,GREEN,BLUE;
	}
	
	public class TestDemo {
		public static void main(String[] args) {
			System.out.println(Color.RED);
		}
	}

实际上枚举就是一种高级的多例设计模式。



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course14)
