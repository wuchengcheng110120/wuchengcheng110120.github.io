## [上一页](course66)

## 接口的定义与使用（接口基本概念）

抽象类与普通类相比最大的特点是约定了子类的实现要求；但是抽象类有一个缺点：单继承局限，如果想要约定子类的实现要求以及避免单继承的局限就需要使用接口。在你以后的开发设计之中：接口优先。在一个操作既可以使用抽象类又可以使用接口的时候请优先考虑接口。

接口就是一个抽象方法和全局常量的集合，在Java中接口可以使用interface关键字来进行定义

**范例** 定义一个接口

	interface IMessage{
		public static final  String MSG = "www.mldn.cn";
		public abstract void print();//抽象方法
	}

但是如果子类想要使用接口，那么就必须利用implements关键字来实现接口，同时一个子类可以实现多个接口，也就是说可以利用接口来实现多继承的概念，对于接口的子类（如果不是抽象类）则必须覆写接口中的全部抽象方法，随后可以利用子类对象的向上转型通过实例化子类来得到接口的实例化对象。

	//因为接口和类的定义命名要求相同，所以为了区分接口建议在所有的接口前面追加一个字母I
	interface IMessage{
		public static final  String MSG = "www.mldn.cn";
		public abstract void print();//抽象方法
	}
	interface INews  {
		public abstract String get() ;
	}
	//一个类现在可以同时实现多个接口
	class MessageImpl implements IMessage, INews{
		public void print() {
			System.out.println(IMessage.MSG);
		}
		public String get() {
			return IMessage.MSG;//访问常量都建议加上类名称
		}
	}
	
	public class TestDemo {
		public static void main(String[] args) {
			IMessage m = new MessageImpl();//子类为父接口实例化
			m.print();//调用被子类所覆写过的方法
		}
	}

**console：**

	www.mldn.cn	

**范例** 观察接口间的转换

	public class TestDemo {
		public static void main(String[] args) {
			INews m = new MessageImpl();//子类为父接口实例化
			//现在m表示的并不是INews，而是MessageImpl;
			//MessageImpl是IMessage的子类;
			IMessage ms = (IMessage) m;
			System.out.println(m.get());
			ms.print();//调用被子类所覆写过的方法
		}
	}

**console：**

	www.mldn.cn
	www.mldn.cn


**范例**
	class NewsImpl implements INews{
		public String get() {
			return IMessage.MSG;//访问常量都建议加上类名称
		}
	}
	
	public class TestDemo {
		public static void main(String[] args) {
			INews m = new NewsImpl();//子类为父接口实例化
			//现在m表示的并不是INews，而是MessageImpl;
			//MessageImpl是IMessage的子类;
			IMessage ms = (IMessage) m;
			System.out.println(m.get());
			ms.print();//调用被子类所覆写过的方法
		}
	}
当一个子类继承了多个接口之后，并且接口对象通过子类进行实例化，那么这多个父接口之间是允许互相转换的。


![](https://i.imgur.com/CH6Sd7X.png)





## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course68)
