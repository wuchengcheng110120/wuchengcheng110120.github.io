## [上一页](course34)

## 9.2 this关键字（this调用方法）

类中的方法有两种：

- 普通方法： this.方法名称（参数...）

- 构造方法： this（参数...）

**范例：** 调用本类方法

	class Person {
		private String name;
		private int age;
		public Person(String name, int age) {
			//this表示属性,当前对象中的属性
			this.name = name;
			this.age = age;
			//如果不使用this也可以调用本类方法那么this的作用是什么？
			this.print();//调用本类方法
		}
		public void print() {
			System.out.println("**********************");
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

	**********************
	姓名： 张三， 年龄：20

虽然调用本类方法前可以不使用this，但是强烈建议追加this，这样的目的是可以区分方法的定义来源。在方法来自其他类时可以更好的区分。

普通方法和构造方法的最大区别：构造方法在使用关键字new实例化类新对象的时候使用一次，而普通方法是在对象实例化完成后（构造方法已经执行），可以调用多次。

在java中支持类构造方法的互相调用。

**范例** 观察构造方法本身存在的问题：

	class Person {
		private String name;
		private int age;
		//无论调用有参还是无参构造函数都执行一段信息输出
		public Person() {//无参构造
			System.out.println("************  一个新的person类对象产生了  **********");
		}
		public Person(String name) {
			System.out.println("************  一个新的person类对象产生了  **********");
			this.name = name;
		}
		public Person(String name, int age) {
			//this表示属性,当前对象中的属性
			System.out.println("************  一个新的person类对象产生了  **********");
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
			System.out.println(new Person().getInfo());
			System.out.println(new Person("张三").getInfo());
			System.out.println(new Person("张三", 20).getInfo());
		}
	}

**console：**

	************  一个新的person类对象产生了  **********
	姓名： null， 年龄：0
	************  一个新的person类对象产生了  **********
	姓名： 张三， 年龄：0
	************  一个新的person类对象产生了  **********
	姓名： 张三， 年龄：20

 程序中出现有重复的代码，所以这样的操作很明显不应该出现，必须消除重复代码。

**范例** 使用this关键字解决问题：

	class Person {
		private String name;
		private int age;
		//无论调用有参还是无参构造函数都执行一段信息输出
		public Person() {//无参构造
			System.out.println("************  一个新的person类对象产生了  **********");
		}
		public Person(String name) {
			this();//调用本类中的无参构造
			this.name = name;
		}
		public Person(String name, int age) {
			//this表示属性,当前对象中的属性
			this(name); //调用本类中有参构造
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
			System.out.println(new Person().getInfo());
			System.out.println(new Person("张三").getInfo());
			System.out.println(new Person("张三", 20).getInfo());
		}
	} 
**console：**

	************  一个新的person类对象产生了  **********
	姓名： null， 年龄：0
	************  一个新的person类对象产生了  **********
	姓名： 张三， 年龄：0
	************  一个新的person类对象产生了  **********
	姓名： 张三， 年龄：20

虽然实现this可以实现构造方法的互相调用，但是此时有以下的几点要求：

- this（）调用构造方法的语句必须在构造方法的首行；

- 使用this调用构造方法的时候请留有出口

## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course36)
