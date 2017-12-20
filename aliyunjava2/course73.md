## [上一页](course72)

## 匿名内部类

在研究匿名内部类之前，首先观察这样一个程序：

**范例** 观察程序：

	interface IMessage{
		public void print();     
	}
	class MessageImpl implements IMessage{
		public void print () {
			System.out.println("hello world! ");
		}
	}
	public class TestDemo {
		public static void main(String[] args) {
			IMessage msg = new MessageImpl();
			fun(msg);
		}
		public static void fun(IMessage temp) {
			temp.print();
		}
	}
**console：**

	hello world! 

如果说现在MessageImpl子类只使用一次，还有必要将其定义为单独的一个类吗？很明显，这就是种浪费。那么此时就可以利用匿名内部类的概念来解决。

	interface IMessage{
		public void print();     
	}
	public class TestDemo {
		public static void main(String[] args) {
			IMessage msg = new IMessage(){// 匿名内部类
				public void print () {
					System.out.println("hello world! ");
				}
			};
			fun(msg);
		}
		public static void fun(IMessage temp) {
			temp.print();
		}
	}

通过这样的程序可以得出这样的结论，基本上搞匿名内部类都应该是在接口或抽象类的形式上完成。

**范例** 在抽象类中使用匿名内部类：

	abstract class Message{
		public void print() {
			System.out.println(this.getInfo());
		}
		public abstract String getInfo();
	}
	public class TestDemo {
		public static void main(String[] args) {
			fun(new Message(){// 匿名内部类
				public String  getInfo() {
					return "hello world! ";
				}
			});
		}
		public static void fun(Message temp) {
			temp.print();
		}
	}

强调：一个普通类尽量不要再去有子类继承，能够继承的只是抽象类和接口，所以虽然可以在普通类上继续使用匿名内部类的形式来定义子类，但是从正常的开发逻辑上这些是错误的。

**范例** 尽量回避的操作：

	class Message{
		public void print() {
			System.out.println("hello world ! ");
		}
	}
	public class TestDemo {
		public static void main(String[] args) {
			fun(new Message(){// 匿名内部类
				public void  print() {
					System.out.println("www.mldn.cn");
				}
			});
		}
		public static void fun(Message temp) {
			temp.print();
		}
	}

以后能在开发中见到最多的匿名内部类都是在抽象类或接口的基础上完成的。

对于匿名内部类暂时不要过多的花费精力，能看懂代码即可，不作为现在的首选
JDK1.8开始匿名内部类有了改进，后面继续了解。

## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course74)
