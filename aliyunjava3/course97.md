## [上一页](course96)
##  【第14个代码模型】反射与工厂设计模式

工厂设计模式曾经给出过一个原则：如果是你自己所编写的接口，要想取得本接口的实例化对象，最好使用工厂类来设计。

但是也需要知道传统工厂类设计所带来的问题。

**范例** 编写一个传统的工厂类：

	package cn.mldn.demo;
	
	interface IFruit {
		public void eat();
	}
	
	class Apple implements IFruit{
		@Override
		public void eat() {
			System.out.println("【Apple】 吃苹果。");
		}
	}
	
	class Factory{
		private Factory() {}
		public static IFruit getInstance(String className) {
			if ("apple".equals(className)) {
				return new Apple();
			}
			return null;
		}
	}
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			IFruit fruit = Factory.getInstance("apple");
			fruit.eat();
		} 
	}
**console：**

	【Apple】 吃苹果。

但是非常遗憾的问题是：该工厂类在开发中根本就不可能使用；

**范例** 修改工厂类：

	class Factory{
		private Factory() {}
		public static IFruit getInstance(String className) {
			if ("apple".equals(className)) {
				return new Apple();
			}else if ("orange".equals(className)) {
				return new Orange();
			}
			return null;
		}
	}
![](http://ww2.sinaimg.cn/large/0060lm7Tly1fnu6gabwm7j30vg0hkjwm.jpg)

所以传统工厂类的弊端： 关键字new。如果想要处理关键字new带来的问题，最好的做法就是通过反射来完成处理，因为Class类可以使用newInstance()实例化对象，同时Class.forName()能够接收String这个类名称。

**范例** 修改程序：

	package cn.mldn.demo;
	
	interface IFruit {
		public void eat();
	}
	
	class Apple implements IFruit{
		@Override
		public void eat() {
			System.out.println("【Apple】 吃苹果。");
		}
	}
	class Orange implements IFruit{
		@Override
		public void eat() {
			System.out.println("【Orange】 吃橘子。");
		}
	}
	class Cherry implements IFruit{
		@Override
		public void eat() {
			System.out.println("【Cherry】 吃樱桃。");
		}
	}
	
	class Factory{
		private Factory() {}
		public static IFruit getInstance(String className) {
			IFruit fruit = null;
			try {
				fruit = (IFruit)Class.forName(className).newInstance();
			} catch (Exception e) {
				e.printStackTrace();
			} 
			return fruit;
		}
	}
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			IFruit fruit = Factory.getInstance("cn.mldn.demo.Cherry");
			fruit.eat();//依然是同一个功能
		} 
	}
通过反射类改进的工厂模式其最大的特征在于：可以方便子类动态进行子类的扩充操作。而关键字new会造成耦合问题。

但是以上的程序依然存在有缺陷，比如说现在有十万个接口，这种模式就意味着要有十万个工厂，而十万个工厂完成的都是同样的功能，这样就很浪费了，所以使用泛型解决当前问题。

**范例** 通过泛型来处理：

	package cn.mldn.demo;
	
	interface IFruit {
		public void eat();
	}
	interface IMessage{
		public void print();
	}
	
	class MessageImpl implements IMessage{
		@Override
		public void print() {
			System.out.println("www.mldn.cn");
		}
		
	}
	class Apple implements IFruit{
		@Override
		public void eat() {
			System.out.println("【Apple】 吃苹果。");
		}
	}
	class Orange implements IFruit{
		@Override
		public void eat() {
			System.out.println("【Orange】 吃橘子。");
		}
	}
	class Cherry implements IFruit{
		@Override
		public void eat() {
			System.out.println("【Cherry】 吃樱桃。");
		}
	}
	
	class Factory<T>{
		private Factory() {}
		@SuppressWarnings("unchecked")
		public static <T>T getInstance(String className) {
			T obj = null;
			try {
				obj = (T)Class.forName(className).newInstance();
			} catch (Exception e) {
				e.printStackTrace();
			} 
			return obj;
		}
	}
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			IFruit fruit = Factory.getInstance("cn.mldn.demo.Cherry");
			fruit.eat();//依然是同一个功能
			IMessage msg = Factory.getInstance("cn.mldn.demo.MessageImpl");
			msg.print();
		} 
	}

**console：**

	【Cherry】 吃樱桃。
	www.mldn.cn

从实际的开发来讲，工厂类使用泛型之后，就可以更好的为更多的接口进行服务了。

在实际开发之中，如果可以掌握泛型和反射的组合操作，那么对于整体的代码就可以编写出高可用的程序了；

## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course98)
