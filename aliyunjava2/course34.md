## [上一页](course33)

## 9.1 this关键字（this调用属性）


this对于初学者是一个很复杂的关键字，可以调用本类方法（普通、构造）、本类属性、表示当前对象（相对概念）。

使用this表示本类属性

**范例** 观察如下代码：

	class Person {
		private String name;
		private int age;
		public Person(String n, int a) {
			name = n;
			age = a;
		}
		public void setName(String n) {
			 name = n;
		}
		public void setAge(int a) {
			 if(a>0 && a<250) {
				 age = a;
			 }
			 age = 0;
		}
		public String getName() {
			return name;
		}
		public int getAge() {
			return age;
		}
		public String getInfo() {
			return "姓名： " + name + "， 年龄：" + age;
		}
	}
	public class ThisDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			System.out.println(new Person("张三", 20).getInfo());
		}
	
	}

**console：**

	姓名： 张三， 年龄：20

现在给出的参数有一些问题，当前类中的构造方法的核心目的：为类中name和age两个属性进行初始化。但是现在构造方法的参数声明不准确，最好的方法是将参数名称与属性名称统一起来。就可能产生参数与属性同名问题，所以为了明确标记出要使用的是属性还是参数，建议属性前都加上“this”关键字


**范例** 观察如下代码：

	class Person {
		private String name;
		private int age;
		public Person(String name, int age) {
			//this表示属性,当前对象中的属性
			this.name = name;
			this.age = age;
		}
		public void setName(String name) {
			 this.name = name;
		}
		public void setAge(int age) {
			 if(age>0 && age<250) {
				 this.age = age;
			 }
			 this.age = 0;
		}
		public String getName() {
			return this.name;
		}
		public int getAge() {
			return this.age;
		}
		public String getInfo() {
			return "姓名： " + this.name + "， 年龄：" + this.age;
		}
	}
	public class ThisDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			System.out.println(new Person("张三", 20).getInfo());
		}
	
	}

**console：**

	姓名： 张三， 年龄：20

只要在类的方法中访问类中的属性，那么属性前一定要追加“this”关键字的形式，this表示当前属性。

## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course35)
