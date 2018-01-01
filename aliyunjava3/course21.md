## [上一页](course20)
## 接口定义加强

JDK1.8对接口的定义有了加强，但是设计过程中要求按照之前的原则进行编写；

在讲解接口加强之前，分析一个实际的问题。
![](http://ww4.sinaimg.cn/large/0060lm7Tly1fn12nsrnxqj30vf0hi7bj.jpg)

造成此种尴尬局面的核心问题在于：接口只是一个方法的声明，而没有具体的方法实现，而随着时间的推移真的出现了以上问题，那么该接口就将无法继续使用。那么这个时候从JDK1.8开始为了解决这样的问题专门提供了两类新的结构：

- 可以使用default来定义普通方法需要通过对象调用

**范例** 定义普通方法：

	package cn.mldn.demo;
	
	interface IMessage{
		public default void fun(){//追加了普通方法，有方法体了
			System.out.println("hello world");
		}
		public void print();
	}
	class MessageImpl implements IMessage{
		@Override
		public void print() {
			System.out.println("www.mldn.com");
		}
	}
	
	public class TestDemo {
		public static void main(String[] args) {
			IMessage msg =new MessageImpl();
			msg.print();
			msg.fun();
		}
	}


- 可以使用static来定义静态方法，通过接口名就可以调用

**范例** 定义static 方法：

	package cn.mldn.demo;
	
	interface IMessage{
		public default void fun(){//追加了普通方法，有方法体了
			System.out.println("hello world");
		}
		//可以由类名称直接调用
		public static IMessage getInstance() {//定义了静态方法
			return new MessageImpl();
		}
		public void print();
	}
	class MessageImpl implements IMessage{
		@Override
		public void print() {
			System.out.println("www.mldn.com");
		}
	}
	
	public class TestDemo {
		public static void main(String[] args) {
			IMessage msg =IMessage.getInstance();
			msg.print();
			msg.fun();
		}
	}

也就是说整体来讲接口更像抽象类了，比抽象类强大在接口依然可以多继承的关系，而抽象类继续保持单继承。

因为时间长了以后随着代码量的增加，许多的支持就会出现问题，为了解决这种扩充问题，才追加了此类的支持，不属于标准设计，它属于挽救设计。



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course22)
