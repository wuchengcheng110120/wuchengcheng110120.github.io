## [上一页](course46)

##  代码块（普通代码块）

代码块是一个不重要的概念，但是作为结构清楚一下即可。所谓代码块指的是使用了“{}”定义的一段程序代码，代码块根据其定义的位置以及声明的关键字的不同一共可以分为四类：普通代码块、构造块、静态库、同步代码块。

普通代码块：

普通代码块指的是定义在方法中的代码块。

**范例** 观察一个简单程序：

	public class TestDemo {
		public static void main(String args[]) {
			if(true) {//表示该判断一定成立
				int x = 10;//局部
				System.out.println("x = " + x);
			}
			int x = 100;//
			System.out.println("x = " + x);
		}
	}
**console：**

	x = 10
	x = 100

如果说现在你将if语句拿掉就成为普通代码块。

	public class TestDemo {
		public static void main(String args[]) {
			{//直接使用大括号进行了定义，普通代码块
				int x = 10;//局部
				System.out.println("x = " + x);
			}
			int x = 100;//
			System.out.println("x = " + x);
		}
	}

如果现在方法中代码写得过长，但是又要避免变量重名问题，往往会使用普通代码块。

## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course48)
