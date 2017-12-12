## [上一页](course54)

## 继承的定义与使用（继承使用限制）

虽然从本质上来讲继承子类可以对父类操作进行共享，但是从另外一个角度来讲，继承本身也是存在一些限制的。

1、 子类对象在实例化之前，一定会首先实例化父类对象，默认调用父类的构造方法后再调用子类的构造方法进行子类对象实例化。
	
- 必须现有父类，再有后代类；

		class Person{
			public Person() {
				System.out.println("*** Person 类对象创建 ***");
			}
		}
		
		class Student extends Person{
			public Student() {
				System.out.println("*** Student 类对象创建 ***");
			}
		}
		
		public class MyDemo {
			public static void main(String[] args) {
				// TODO Auto-generated method stub
				new Student();
			}
		}

没有任何语句明确调用父类构造，但是父类构造仍然被执行了，所以证明子类对象的实例化一定会实例化其父类对象。

但是需要注意的是，实际上这个时候在子类的构造方法之中相当于隐含了一个语句“super（）”

	class Student extends Person{
		public Student() {
			//既然要进行构造方法的调用，构造方法的调用语句一定要放在构造方法的首行
			super();//此语句在无参时写与不写一样
			System.out.println("*** Student 类对象创建 ***");
		}
	}

但是同时需要注意的是，此时父类中如果没有提供无参构造，那么这个时候必须使用super（）明确你要调用的父类构造方法。

	class Person{
		public Person(String name , int age) {//有参构造
			System.out.println("*** Person 类对象创建 ***");
		}
	}
	
	class Student extends Person{
		public Student(String name, int age,String school) {
			super(name,age);//明确定义要调用的父类构造
			System.out.println("*** Student 类对象创建 ***");
		}
	}
	
	public class MyDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			new Student("MLDN",10,"清华大学");
		}
	}

**console：**

	*** Person 类对象创建 ***
	*** Student 类对象创建 ***

2、 java中只允许单继承，不允许多继承；

一个子类只能够继承一个父类

**范例** 错误的多继承：

	class A{}
	
	class B{}
	
	class C extends A,B{
		
	}

实际上C类要同时继承A,B的目的是为了同时拥有A和B类中的操作，所以为了实现这样的目的，可以采用多层继承的形式完成。


	class A{}
	
	class B extends A{}
	
	class C extends B{
		
	}

但是不建议继承过多层，建议多层继承不要超过三层。

总结： java不允许多重继承，但是允许多层继承。

3、 在进行继承的时候，子类会继承父类的所有结构，但是这个时候需要注意的是，所有的非私有操作属于显式继承（可以直接调用），而所有的私有操作属于隐式继承（通过其他形式调用，例如：setter，getter）

	class Person{
		private String name;
		private int age;
		public void setName(String name) {
			this.name = name;
		}
		public void setAge(int age) {
			this.age = age;
		}
		public String getName() {
			return this.name;
		}
		public int getAge() {
			return this.age;
		}
	}
	
	class Student extends Person{//定义了一个子类
		private String school;
		public void setSchool(String school) {
			this.school = school;
		}
		public String getSchool() {
			return this.school;
		}
		public void fun() {
			System.out.println(getName());
		}
	}
	
	public class TestDemo {
		public static void main(String args[]) {
			Student stu = new Student(); //实例化子类
			stu.setName("张三");
			System.out.println(stu.getName());
			stu.fun();
		}
	}

此时父类中的属性的确被子类继承了，但是发现子类能够使用的只是所有的非private操作（public），而所有的private操作肯定无法直接使用，所以称为隐式继承。


1、 继承的语法和继承的目的（扩展已有类的功能，是代码重用）；

2、 子类对象的实例化流程：不管如何操作，一定要实例化父类对象，再实例化子类对象；

3、 继承的限制：不允许多重继承，只允许多层继承。


## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course56)
