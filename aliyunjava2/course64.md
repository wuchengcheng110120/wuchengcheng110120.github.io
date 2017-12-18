## [上一页](course63)

## 抽象类的定义与使用（抽象类基本概念）

【90%的正规代码】在以后的开发过程中，绝对不要出现一个类去继承一个已经实现好的类，而只能继承抽象类和接口。

对象多态性的核心本质在于方法的覆写上，如果说现在的子类没有去进行指定方法的覆写，这样的操作就有些不合乎要求了。所以如果要对子类的方法进行一些强制的要求，就必须采用抽象类来解决。

抽象类只是在普通类的基础上扩充了一些抽象方法而已。所谓的抽象方法指的是只声明而未实现的方法，所有的抽象方法要求使用abstract关键字来进行定义，并且抽象方法所在的类也一定要使用abstract定义类，表示抽象类。

**范例** 定义一个抽象类

	abstract class  A {
		private String msg = "www.mldn.cn";//属性
		public void print() {//普通方法
			System.out.println(msg);
		}
		public void a() {}
		//{}为方法体，所以说所有的抽象方法上是不包含方法体的
		public abstract void fun();//抽象方法
	}
	
抽象类就是比普通类多了一些抽象方法而已。

抽象类中包含有抽象方法，而抽象方法与普通方法的最大区别在于其没有方法体，即：不知道具体的实现，如果现在产生了实例化对象则意味着可以调用类中的左右操作。

对于抽象类使用的原则：

- 所有的抽象类必须要有子类；

- 抽象类的子类（不是抽象类）必须全部覆写抽象类的抽象方法；
	
	|- 方法覆写一定要考虑权限问题：抽象方法可以使用任意权限，要求权限尽量都用public

- 抽象类的对象可以通过对象多态性，利用子类为其实例化；

**范例** 使用抽象类：

	abstract class  A {
		private String msg = "www.mldn.cn";//属性
		public void print() {//普通方法
			System.out.println(msg);
		}
		public void a() {}
		//{}为方法体，所以说所有的抽象方法上是不包含方法体的
		public abstract void fun();//抽象方法
	}
	//一个子类只能够利用extends来继承抽象类，所以仍然存在单继承局限；
	class B extends A{//定义抽象类的子类
		public void fun() {
			System.out.println("hello world !");
		}
	}
	public class TestDemo {
		public static void main(String[] args) {
			A a = new B();//实例化子类对象
			a.fun();
		}
	}
**console：**

	hello world !

从正常的开发角度来讲，以上的操作没有任何问题，而且也是一种使用最多的形式，但是对于抽象类必须有一点说明，以后可能见到如下的一种使用形式。

	abstract class  A {
		private String msg = "www.mldn.cn";//属性
		public void print() {//普通方法
			System.out.println(msg);
		}
		public static A getInstance() {//取得A类对象
			class B extends A{//定义抽象类的子类(内部类)
				public void fun() {
					System.out.println("hello world !");
				}
			}
			return new B();
		}
		//{}为方法体，所以说所有的抽象方法上是不包含方法体的
		public abstract void fun();//抽象方法
	}
	public class TestDemo {
		public static void main(String[] args) {
			A a = A.getInstance();//实例化子类对象
			a.fun();
		}
	}


此类模式属于非正常模式，但是对于一些封装性是有好处的。


## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course65)
