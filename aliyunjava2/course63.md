## [上一页](course62)

## 多态性

我们学习完了继承的概念，并不意味着只要使用继承就可以实现代码的全部重用，在继承之后又有一个重要的核心概念：多态性；

在java里面对与多态的核心表现主要有以下两点：

- 方法的多态性：

	|- 方法的重载：同一个方法名称可以根据参数类型及个数的不同调用不同的方法体；

	|- 方法的覆写：同一个父类的方法，可能根据实例化的子类不同也有不同的实现；

- 对象的多态性（前提：方法覆写）：

	|- 【自动，90%】对象的向上转型： 父类 父类对象 = 子类实例；

	|- 【强制，1%】对象的向下转型： 子类 子类对象 = （子类）父类实例；

		|- 9% 是不进行转型，例如String；

**范例** 回顾一个简单程序：

	class  A {
		public void print() {
			System.out.println("【A】 public void print(){}");
		}
	}
	class  B extends A {
		public void print() {
			System.out.println("【B】 public void print(){}");
		}
	}
	public class TestDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			B b = new B();//实例化子类对象
			b.print();//调用被覆写过的方法
		}
	}
**console：**

	【B】 public void print(){}

于是可以将以上代码进一步变化，变为向上转型；

**范例** 实现向上转型：

	class  A {
		public void print() {
			System.out.println("【A】 public void print(){}");
		}
	}
	class  B extends A {
		public void print() {
			System.out.println("【B】 public void print(){}");
		}
	}
	public class TestDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			A a = new B();//向上转型
			a.print();//调用被覆写过的方法
		}
	}

**console：**

	【B】 public void print(){}

不管是否发生了向上转型，其核心本质还是在于：使用的是哪一个子类（new在哪里），调用的子类方法是否被覆写。

向下转型指的是将父类对象变为子类对象，但是在这之前，需要首先明确一个核心概念，为什么需要向下转型？当你需要使用到子类扩充操作的时候就要采用向下转型。

**范例** 向下转型：

	class  A {
		public void print() {
			System.out.println("【A】 public void print(){}");
		}
	}
	class  B extends A {
		public void print() {
			System.out.println("【B】 public void print(){}");
		}
		public void funB() {
			System.out.println("【B】 public void funB(){}");
		}
	}
	public class TestDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			A a = new B();//向上转型
			a.print();
			//这个时候父类能够调用的方法只能是自己本类定义好的方法
			//所以这个时候并没有B类中的funB（）方法，那么只能够进行向下转型处理；
			B b = (B)a;
			b.funB();//调用被覆写过的方法
		}
	}
**console：**

	【B】 public void print(){}
	【B】 public void funB(){}

【此概念一般开发中用不到】但是并不是所有的父类对象都可以向下转型：如果要想进行向下转型操作之前一定要先进行向上转型，否则在转型时会出现：ClassCastException。

**范例** 错误的转型：

	class  A {
		public void print() {
			System.out.println("【A】 public void print(){}");
		}
	}
	class  B extends A {
		public void print() {
			System.out.println("【B】 public void print(){}");
		}
		public void funB() {
			System.out.println("【B】 public void funB(){}");
		}
	}
	public class TestDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			A a = new A();//实例化父类对象
			B b =  (B) a;
			
		}
	}

**console：**

	Exception in thread "main" java.lang.ClassCastException: bznoc171118.A cannot be cast to bznoc171118.B
		at bznoc171118.TestDemo.main(TestDemo.java:20)
	
但是现在就有一个问题出现了，如果向下转型可能存在有隐患，那么如何转型最靠谱呢？最好的做法是先进行判断，而后在进行转型，那么就可以依靠instanceof关键字来实现了，此关键字的使用语法如下：

- 子类对象 instanceof类， 返回的是boolean型数据；

**范例** 观察instanceof关键字使用：

	public class TestDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			A a = new B();
			System.out.println(a instanceof A);
			System.out.println(a instanceof B);
			//以后对于子类的特殊操作尽量慎用
			if (a instanceof B) {//避免ClassCastException
				B b = (B) a;
				b.funB();
			}
		}
	}

**console：**

	true
	true
	【B】 public void funB(){}

虽然清楚了这一系列的操作关系，可是还必须思考，这种转换有什么意义？

**范例** 要求定义一个方法，而这个方法可以接收Person类的所有子类实例，并调用Person类的方法； 

	class  Person {
		public void takeoff() {//脱
			System.out.println("脱掉...");
		}
	}
	class  Student extends Person {
		public void takeoff() {//脱
			System.out.println("一件件脱...");
		}
	}
	
	class  Worker extends Person {
		public void takeoff() {//脱
			System.out.println("直接卷...");
		}	
	}
	
	public class TestDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			in(new Student());
			in(new Worker());
		}
		public static void in(Person per) {
			per.takeoff();//所有的人不管什么职业都按照统一的动作进行
		}
	}

**console：**

	一件件脱...
	直接卷...

通过以上分析就可以清楚，对象的向上转型有一个最为核心的用途：操作参数统一。

1、对象多态性实现的核心在于方法的覆写；

2、通过对象的向上转型可以实现接收参数的统一，而向下转型可以实现子类扩充方法的调用（一般不操作向下转型）；

3、两个没有继承关系的对象是不能够进行转型的，一定会发生ClassCastException，所以向下转型是存在有安全隐患的。

## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course64)
