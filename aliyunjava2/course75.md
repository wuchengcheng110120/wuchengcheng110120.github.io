## [上一页](course74)

## Object类（取得对象信息）

在使用对象直接输出的时候发现默认的输出对象是一个地址编码，但是如果说使用的是一个String类，该类对象直接输出的时候就是内容，主要的原因就是toString（）方法问题。

**范例**观察String类对象的输出：

	class Person{
		private String name;
		private int age;
		public Person(String name, int age) {
			this.name = name;
			this.age = age;
		}
	}
	public class TestDemo {
		public static void main(String[] args) {
			fun("hello");//String 是Object类的子类
			fun(new Person("张三", 20));//自定义对象
		}
		public static void fun(Object obj) {//所有的类对象都可以进行接收
			System.out.println(obj);
		}
	}

**console：**

	hello
	bznoc171118.Person@52e922


修改后：

	public class TestDemo {
		public static void main(String[] args) {
			fun("hello");//String 是Object类的子类
			fun(new Person("张三", 20));//自定义对象
		}
		public static void fun(Object obj) {//所有的类对象都可以进行接收
			System.out.println(obj.toString());//默认输出对象调用的就是toString（）方法
		}
	}
**console：**

	hello
	bznoc171118.Person@52e922

现在发现了默认情况下Object类中提供的toString（）方法只能够得到一个对象的地址（而这是所有对象共同具备的特征）。

而现在如果觉得默认给出的toString（）功能不足，就建议在需要的子类上覆写toString（）方法。
**范例** 覆写toString（）：

	class Person{
		private String name;
		private int age;
		public Person(String name, int age) {
			this.name = name;
			this.age = age;
		}
		public String toString() {//覆写Object类中的方法
			return "姓名： "  + this.name +  ", 年龄： "   +  this.age ;
		}
	}
	public class TestDemo {
		public static void main(String[] args) {
			fun("hello");//String 是Object类的子类
			fun(new Person("张三", 20));//自定义对象
		}
		public static void fun(Object obj) {//所有的类对象都可以进行接收
			System.out.println(obj.toString());//默认输出对象调用的就是toString（）方法
		}
	}

**console：**

	hello
	姓名： 张三, 年龄： 20

所以toString（）的核心目的在于取得对象信息。相当于替换了简单Java类中的getInfo（）方法的功能。

提醒： String是作为信息输出的重要的数据类型，在Java中所有的数据类型只要遇见了String，并且执行了“+”这种连接操作，那么都要求将其变为字符串后连接，而所有对象要想变为字符串就默认使用toString（）方法。

**范例** String + 对象（默认调用toString（）方法）： 

	public class TestDemo {
		public static void main(String[] args) {
			String result = "Hello " + new Person("张三", 20);
			System.out.println(result);
		}
	}

**console：**

	Hello 姓名： 张三, 年龄： 20



## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course76)
