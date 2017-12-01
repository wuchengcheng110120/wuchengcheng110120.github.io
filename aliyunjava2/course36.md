## [上一页](course35)

## 9.3 this关键字（this表示当前对象）

在一个类之中肯定会产生若干个对象，程序在分辨的时候不会记住有多少个对象产生了，而是会记住操作本类的对象是哪一个。

**范例**  观察当前对象;

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
		public void fun() {
			System.out.println(" 【FUN方法】 " + this);
		}
		
	}
	public class ThisDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			Person p1 = new Person();
			System.out.println(" 【MAIN方法】 "+ p1);
			p1.fun();
			System.out.println("======================");
			Person p2 = new Person();
			System.out.println(" 【MAIN方法】 "+ p2);
			p2.fun();
		}
	}

**console :**

	************  一个新的person类对象产生了  **********
	 【MAIN方法】 bznoc171118.Person@52e922
	 【FUN方法】 bznoc171118.Person@52e922
	======================
	************  一个新的person类对象产生了  **********
	 【MAIN方法】 bznoc171118.Person@25154f
	 【FUN方法】 bznoc171118.Person@25154f

在操作的过程中，this定义没有变，只要有某一个对象调用了本类的方法，this就表示当前执行的对象。

## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course37)
