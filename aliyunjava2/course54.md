## [上一页](course53)

## 继承的定义与使用（继承的实现）

java中继承使用extends关键字来实现，其定义的语法如下：

- 继承关系： class 子类 extends 父类；

	|- 子类在一些书上也被称为派生类；
	
	|- 父类也被称为超类（Super Class）。

**范例**  继承的基本实现：

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
		
	}
	
	public class TestDemo {
		public static void main(String args[]) {
			Student stu = new Student(); //实例化子类
			stu.setName("啊天");
			stu.setAge(6);
			System.out.println("姓名：" + stu.getName() + "， 年龄： " + stu.getAge());
		}
	}
	
**console：**

	姓名：啊天， 年龄： 6

通过此时的代码可以发现，在发生继承关系之后，子类可以直接继承父类的操作，也就是说可以实现代码的重用，并且子类最低也维持和父类相同的功能。当然子类也可以进行功能的扩充，例如属性和方法。

**范例** 子类进行功能的扩充：

	class Student extends Person{//定义了一个子类
		private String school;
		public void setSchool(String school) {
			this.school = school;
		}
		public String getSchool() {
			return this.school;
		}
	}
	
	public class TestDemo {
		public static void main(String args[]) {
			Student stu = new Student(); //实例化子类
			stu.setName("啊天");
			stu.setAge(6);
			stu.setSchool("卡里吨大学");
			System.out.println("姓名：" + stu.getName() + "， 年龄： " + stu.getAge()
			+ ", 学校： " + stu.getSchool());
		}
	}

**console：**

	姓名：啊天， 年龄： 6, 学校： 卡里吨大学

通过上述代码可以发现，继承的确可以进行父类功能的扩充，并且最重要的是可以重用父类中定义的方法，继承的主要功能是对类进行扩充。

## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course55)

