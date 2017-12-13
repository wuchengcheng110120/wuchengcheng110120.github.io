## [上一页](course55)

## 覆写（方法覆写）

清楚了继承的概念，那么此时就有可能出现这样的一种情况，如果子类定义了与父类相同的方法或者是属性的时候，这样的操作就称为覆写。

- 属性的覆盖

- 方法的覆写

所谓的方法的覆写指的是子类定义了与父类方法名称、参数类型及个数完全相同的方法。但是被覆写的方法不能够拥有比父类更严格的访问控制权限。

**范例** 观察简单的方法覆写：

	class Person{
		public void printInfo() {
			System.out.println("1、 【Person 类】 printInfo() 方法");
		}
	}
	
	class Student extends Person{//定义了一个子类
		//在你们开发之中，99%的情况下子类的方法名称和父类中的方法名称是完全一样的
		public void printInfo() {
			System.out.println("2、【Student 类】 printInfo() 方法");
		}
	}
	
	public class TestDemo {
		public static void main(String args[]) {
			Student stu = new Student(); //实例化子类
			stu.printInfo();
		}
	}
**console：**

	2、【Student 类】 printInfo() 方法

进行覆写方法使用的时候一定要关注以下两点：

- 当前使用的对象是使用哪个类new出来的

- 当调用某一个方法，如果该方法已经被子类覆写了，则调用覆写过的方法；

	class Worker extends Person{
		public void printInfo() {
			System.out.println("3、【Worker 类】 printInfo() 方法");
		}
	}
	
	public class TestDemo {
		public static void main(String args[]) {
			Worker stu = new Worker(); //实例化子类
			stu.printInfo();
		}
	}

**console：**

	3、【Worker 类】 printInfo() 方法

但是在进行方法覆写的时候也有一个明确的要求：被覆写的方法不能有比父类更为严格的访问控制权限。关于访问控制权限才是封装的全部内容，现在已经接触过了三种访问控制权限：private(个人) < default（教师） < public（国家新闻） ;

如果说父类中使用了public定义，子类中只能使用public定义，如果父类中使用default权限，子类可以使用default或public。

**范例** 错误的覆写：

	class Person{
		public void printInfo() {
			System.out.println("1、 【Person 类】 printInfo() 方法");
		}
	}
	class Student extends Person{//定义了一个子类
		 void printInfo() {
			System.out.println("2、【Student 类】 printInfo() 方法");
		}
	}

结论：以后方法尽量写public权限，至少能保证不会出现权限问题；

同时写属性尽量都写private；

问题：如果现在父类中的方法使用private定义，子类中使用了public覆写，会怎样？

- 从概念上来讲，父类的方法使用了private，子类的方法使用了public，那么这属于权限扩大

	class Person{
		public void fun() {
			this.printInfo();
			this.printInfo1();
		} 
		//如果父类中的方法使用了private定义，那就表示该方法只能够被父类所使用
		//，子类无法使用，也就是说子类并不知道父类有这样的方法
		private void printInfo() {
			System.out.println("1、 【Person 类】 printInfo() 方法");
		}
		public void printInfo1() {
			System.out.println("1、 【Person 类】 printInfo1() 方法");
		}
	}
	class Student extends Person{
		//这个时候该方法只是子类定义的新方法而已，和父类的方法没有任何关系
		public void printInfo() {
			System.out.println("2、 【Student 类】 printInfo() 方法");
		}
		public void printInfo1() {
			System.out.println("2、 【Student 类】 printInfo1() 方法");
		}
	}
	public class TestDemo {
		public static void main(String args[]) {
			Student stu = new Student(); //实例化子类
			stu.fun();
		}
	}

**console：**

	1、 【Person 类】 printInfo() 方法
	2、 【Student 类】 printInfo1() 方法

请解释覆写与重载的区别，在进行重载的时候返回值是否可以不同？：

no | 区别 | 重载 | 覆写
-|---|-|-
 1| 英文 | overloading | override |
 2 | 概念 | 方法名称相同，参数名称、个数不同 | 方法名称、返回值类型、参数名称个数相同 |
 3 | 范围 | 发生在一个类之中 | 发生在继承关系中|
 4 | 限制 | 没有权限要求 | 被覆写的方法不能拥有比父类更为严格的访问控制权限
 
方法重载的时候返回值可以不同，但是良好的设计要求返回类型一致。

## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course57)
