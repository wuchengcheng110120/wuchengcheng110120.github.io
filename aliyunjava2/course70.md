## [上一页](course69)

## 接口的定义与使用（工厂设计模式）

### Factory、重点

Java常用的设计模式：工厂、代理、单例；

首先来看一个简单的程序范例：在进行类设计的时候，要求首先需要有接口，而后接口要通过子类才可以进行对象的实例化处理。

**范例** 传统代码开发：

	interface IFruit{//定义一个描述水果的操作
		public void eat();//吃水果
	}
	class Apple implements IFruit{
		public void eat() {
			System.out.println("削皮吃苹果！ ");
		}
	}
	public class TestDemo {
		public static void main(String[] args) {
			//子类为接口进行实例化处理
			IFruit fruit = new Apple();
			fruit.eat();
		}
	}

**console：**

	削皮吃苹果！ 

此时的程序实现的关键是“IFruit fruit = new Apple();”，如果没有此语句接口对象将无法进行实例化的操作处理，但是最大的败笔也在此。主方法是一个客户端，对于程序的修改不应该影响到客户端。

Java实现可移植性的关键是JVM，也就是说所有的程序是在JVM上执行，而不同的操作系统中有匹配的JVM，相当于：

	程序 ——> JVM ——> 操作系统

这个时候new使整个开发过程中最大的耦合元凶，而在开发之中进行解耦合的关键就在于要引入一个第三方，所以这个类可以使用Factory来描述。

**范例** 通过Factory设计：

	interface IFruit{//定义一个描述水果的操作
		public void eat();//吃水果
	}
	class Factory {
		//因为此时Factory 产生实例化对象没有意义
		public static IFruit getInstance(String className) {
			if ("apple".equals(className)) {
				return new Apple();
			}
			if ("orange".equals(className)) {
				return new Orange();
			}
			return null;
		}
	}
	class Apple implements IFruit{
		public void eat() {
			System.out.println("削皮吃苹果！ ");
		}
	}
	class Orange implements IFruit{
		public void eat() {
			System.out.println("剥皮吃橘子！ ");
		}
	}
	public class TestDemo {
		public static void main(String[] args) {
			if (args.length != 1) {//没有传递一个参数
				System.out.println("对不起，程序执行错误，正确的格式："
						+ "java TestDemo 类名称");
				System.exit(1);//退出程序执行
			}
			IFruit fruit = Factory.getInstance(args[0]);
			fruit.eat();
		}
	}

当更换使用的IFruit子类的时候主方法没有任何变化就可以实现了子类的变更，这样的设计就成为工厂设计模式。

**总结：**

以后编写的接口如果要取得接口的实例化对象，第一反应写工厂类


## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course71)
