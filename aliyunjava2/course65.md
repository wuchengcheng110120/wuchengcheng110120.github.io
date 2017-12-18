## [上一页](course64)

## 抽象类的定义与使用（抽象类使用限制）

1、 抽象类只是比普通类多了一些抽象方法的定义而已，所以抽象类中依然允许提供有构造方法，并且子类也会遵守子类对象的实例化流程，实例化子类对象前一定要先去调用父类的构造方法。

**范例** 在抽象类中定义构造方法：

	abstract class Person{
		private String name;
		private int age;
		public Person() {
			System.out.println("******************");
		}
		public abstract String getInfo();
	}
	class Student extends Person {
		private String school;
		public Student() {
			System.out.println("#################");
		}
		public String getInfo() {
			return null;
		}
	}
	public class TestDemo {
		public static void main(String[] args) {
			new Student();
		}
	}
**console：**

	******************
	#################

如果说现在父类中没有无参构造，那么子类就必须通过super（）指明要调用的父类构造方法。

	abstract class Person{
		private String name;
		private int age;
		public Person(String name, int age) {
			this.name =name;
			this.age = age;
			System.out.println("******************");
		}
		public String getName() {
			return this.name;
		}
		public int getAge() {
			return this.age;
		}
		public abstract String getInfo();
	}
	class Student extends Person {
		private String school;
		public Student(String name, int age,String  school) {
			super(name, age);//子类构造必须明确调用父类构造
			this.school = school;
		}
		public String getInfo() {
			return "【Student】 name = " + super.getName() + "、 age = "+ super.getAge() 
			+ "、school = " + this.school;
		}
	}
	public class TestDemo {
		public static void main(String[] args) {
			Person per = new Student("张三",20 , "北京大学");
			System.out.println(per.getInfo());
		}
	}
**console：**

	******************
	【Student】 name = 张三、 age = 20、school = 北京大学

其实抽象类中存在有构造方法也很好理解，毕竟抽象类中还有属性，所有的属性一定要在对象实例化的时候进行空间开辟，对象实例化必须要使用构造方法。

额外话题：关于对象实例化

对象的实例化操作实际上需要以下几个核心步骤：

- 进行类的加载；

- 进行类对象的空间开辟；

- 进行类对象中的属性初始化（构造方法）；
	
		abstract class A{
			public A() {//3、 调用父类构造方法
				this.print();//4、 调用被子类覆写过的抽象方法
			}
			public abstract void print();//抽象方法
		}
		class B extends A{
			private int num =100;
			public B(int num) {//2、 调用子类实例化对象
				super(); //3、 隐含一行语句，实际上要调用父类构造
				this.num =num;//7、 为类中的属性初始化
			}
			public void print() {//5、 此时子类对象还没有被初始化
				System.out.println(this.num);//6、 内容其对应数据类型的默认值
			}
		}
		public class TestDemo {
			public static void main(String[] args) {
				new B(30);//1、 实例化子类对象
			}
		}


构造方法没执行之前，所有属性都是其对应类型的默认值；

2、 抽象类中允许不定义任何的抽象方法，但是此时抽象类对象依然无法进行直接实例化处理

abstract class A{
	public void print() {}
}

public class TestDemo {
	public static void main(String[] args) {
		A a = new A();//错误A是抽象的，无法进行实例化
	}
}


3、 抽象类一定不能够使用final进行声明，因为使用final定义的类不能有子类，而抽象类必须有子类。

- 抽象方法不能使用private定义，因为抽象方法必须被覆写；

4、 抽象类也分为内部抽象类和外部抽象类，内部抽象类中可以使用static定义描述为外部抽象类。

**范例：** 观察内部抽象类：

	abstract class A{//此类结构出现几率很低
		public abstract void printA();
		abstract class B{
			public abstract void printB();
		}
	}
	class X extends A{
		public void printA() {}
		class Y extends B {
			public void printB() {}
		}
	}

而如果现在外部抽象类上使用了static那么就是语法错误，可内部抽象类上允许使用static

	abstract class A{//此类结构出现几率很低
		public abstract void printA();
		static abstract class B{
			public abstract void printB();
		}
	}
	class X extends A.B{
		public void printB() {}
	}

从一般的设计角度来讲，以上的问题很多时候并不会出现。



## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course66)
