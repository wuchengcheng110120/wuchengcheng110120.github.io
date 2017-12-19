## [上一页](course67)

## 接口的定义与使用（接口使用限制）


1、 接口一旦定义完成之后，就需要对其有一个核心的说明，那么首先需要说明的是：接口里面只允许存在public权限，也就是说，不管是属性还是方法其权限永恒都是public。

**范例** 错误的覆写：

	interface INews  {
		 abstract String get() ;//即便不写public，也是public
	}
	
	class NewsImpl implements INews{
		String get() {//权限更加严格了所以无法覆写
			return "www.mldn.cn";//访问常量都建议加上类名称
		}
	}

在以前给过一个核心总结：只要是方法就使用public定义，而你如果遵守了这一要求这些问题都可以回避，另外由于接口之中只是全局常量和抽象方法的集合，所以一下的两种的定义形式效果都是一样的：

   	完整格式

	interface INews  { 
		public static final String MSG = "www.mldn.cn";
		public abstract String get() ;//即便不写public，也是public
	}

	简化格式

	interface INews  { 
		String MSG = "www.mldn.cn";
		String get() ;//即便不写public，也是public
	}

在以后编写接口的时候，99%的接口中只会提供有抽象方法，很少会在接口里面看到有许多的全局常量的。所以很多的时候为了避免开发者出现混乱，所以接口的方法上往往都会加上public

2、 当一个子类需要实现接口又需要是实现类的时候，请先使用extends继承一个抽象类再使用implements实现多个接口

**范例** 集成一个抽象类实现多个接口：

	interface INews  {
		public static final String MSG = "www.mldn.cn";
		public abstract String get() ;//即便不写public，也是public
	}
	//可以在类上进行明确描述，在开发中也经常出现以下的命名习惯
	abstract class AbstractMessage{
		//只有接口中的abstract才可以省略，抽象类中不能省略
		public abstract void print();
	}
	
	class NewsImpl extends AbstractMessage implements INews{
		public String get() {//权限更加严格了所以无法覆写
			return "www.mldn.cn";//访问常量都建议加上类名称
		}
		public void print() {}//有方法体就称为覆写
	}
	public class TestDemo {
		public static void main(String[] args) {
			INews news = new NewsImpl();//子类为父接口实例化
			System.out.println(news.get());
			//NewsImpl是抽象类和接口的共同子类
			AbstractMessage am = (AbstractMessage) news;
			am.print();
		}
	}

**console:**
 
	www.mldn.cn

3、 一个抽象类可以使用implements实现多个接口，但是接口不能去继承抽象类

	interface INews  {
		public static final String MSG = "www.mldn.cn";
		public abstract String get() ;//即便不写public，也是public
	}
	//可以在类上进行明确描述，在开发中也经常出现以下的命名习惯
	abstract class AbstractMessage implements INews{
		//只有接口中的abstract才可以省略，抽象类中不能省略
		public abstract void print();
	}
	class NewsImpl extends AbstractMessage {
		public String get() {//权限更加严格了所以无法覆写
			return "www.mldn.cn";//访问常量都建议加上类名称
		}
		public void print() {}//有方法体就称为覆写
	}
	public class TestDemo {
		public static void main(String[] args) {
			INews news = new NewsImpl();//子类为父接口实例化
			System.out.println(news.get());
			//NewsImpl是抽象类和接口的共同子类
			AbstractMessage am = (AbstractMessage) news;
			am.print();
		}
	}

实际上此时的关系属于三层继承

	interface INews  {
		public static final String MSG = "www.mldn.cn";
		public abstract String get() ;//即便不写public，也是public
		public void print();
	}
	//可以在类上进行明确描述，在开发中也经常出现以下的命名习惯
	abstract class AbstractMessage implements INews{
		//只有接口中的abstract才可以省略，抽象类中不能省略
		public void print() {
			System.out.println("www.mldn.cn");
		}
	}
	class NewsImpl extends AbstractMessage implements INews {
		public String get() {//权限更加严格了所以无法覆写
			return "www.mldn.cn";//访问常量都建议加上类名称
		}
	}
	public class TestDemo {
		public static void main(String[] args) {
			INews news = new NewsImpl();//子类为父接口实例化
			System.out.println(news.get());
			//NewsImpl是抽象类和接口的共同子类
			AbstractMessage am = (AbstractMessage) news;
			am.print();
		}
	}

**console：**

	www.mldn.cn
	www.mldn.cn

![](https://i.imgur.com/XwbPq3c.png)

4、 一个借口可以使用extends来继承多个父接口

	interface A{
		public void printA();
	}
	interface B{
		public void printB();
	}
	interface C extends A,B {
		public void printC();
	}
	class Impl implements C{
		public void printA() {}
		public void printB() {}
		public void printC() {}
	}

5、 接口可以定义一系列的内部接口，包括：内部普通类、内部抽象类、以及内部接口，其中使用static定义的内部接口就相当于一个外部接口；

	interface A{
		static interface B{//使用static定义描述了一个外部接口
			public void printB();
		}
	}
	class X implements A.B{//实现内部接口
		public void printB() {}
	}

内部结构不是程序设计的首选，而且要想清楚接口的实际开发意义，需要大量的项目来验证。





## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course69)
