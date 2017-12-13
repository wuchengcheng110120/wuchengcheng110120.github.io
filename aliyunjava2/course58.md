## [上一页](course57)

## 覆写（super关键字）

在子类对象实例化操作的时候讲解过了super（）的形式，当时的主要作用是由子类调用父类构造方法时才使用的，那么在进行覆写的过程中，子类也可以使用super.方法（）、super.属性明确的调用父类的方法和属性。

**范例** 观察一个程序：

	class Person{
		public void printInfo() {
			System.out.println("111111111111111111");
		}
	}
	class Student extends Person{
		public void printInfo() {
			//this.printInfo();
			super.printInfo();
			System.out.println("222222222222222222222222222");
		}
	}
	public class TestDemo {
		public static void main(String args[]) {
			Student stu = new Student(); //实例化子类
			stu.printInfo();
		}
	}

**console：**

	111111111111111111
	222222222222222222222222222

如果直接写上“this.printInfo（）”操作，那么就表示先从本类查找所需要的方法，如果本类没有则去找父类中的方法进行调用，而如果加上“super.printInfo（）”表示不查找本类而直接调用父类中的方法。

**范例** 调用父类属性：

	class Person{
		public String info = "www.mldn.cn";
	}
	class Student extends Person{
		public int info = 100;
		public void printInfo() {
			System.out.println(super.info);
			System.out.println(info);
		}
	}
	public class TestDemo {
		public static void main(String args[]) {
			Student stu = new Student(); //实例化子类
			stu.printInfo();
		}
	}

**console：**

	www.mldn.cn
	100

通过一系列的讲解发现super和this使用形式上非常相似，但是两者最大的区别是super是子类访问父类的操作，而this是本类的访问处理操作。


no | 区别 | this | super
-|---|-|-
 1 | 概念 | 访问本类中的属性和方法  | 由子类访问父类中的属性和方法  |
 2 | 查找范围 | 先查找本类，如果本类没有则调用父类 | 不查找本类直接调用父类定义
 3 | 特殊 | 表示当前对象 |  无

能使用super.方法（）一定要明确的标记出是父类的操作。


1、 子类覆写父类的方法是因为父类的方法功能不足，才需要覆写；

2、 方法覆写的时候使用的就是public权限，将父类的方法名称直接粘贴

## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course59)
