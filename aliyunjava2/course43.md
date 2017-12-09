## [上一页](course42)

##  static关键字（static 属性）

在所有定义的属性和方法上都可以使用static关键字进行定义。

讲解具体的static操作之前先观察这样一个程序：

**范例** 定义一个表示人的类，同时设置他所在的国家：

	class Person {
		private String  name;
		private int age;
		String country = "中国";   //为了后面的操作放笔恩，暂时不封装
		public Person(String name, int age) {
			this.name = name;
			this.age = age;
		}
		
		public String getInfo() {
			return "姓名： " + this.name + ", 年龄 ：" + this.age + ", 国家： " + this.country ;
		}
	}
	
	public class TestDemo {
		public static void main(String args[]) {
			Person p1 = new Person("张三", 10);
			Person p2 = new Person("李四", 11);
			Person p3 = new Person("王五", 12);
			System.out.println(p1.getInfo());
			System.out.println(p2.getInfo());
			System.out.println(p3.getInfo());
		}
	}
		
**console：**

	姓名： 张三, 年龄 ：10, 国家： 中国
	姓名： 李四, 年龄 ：11, 国家： 中国
	姓名： 王五, 年龄 ：12, 国家： 中国

这种定义模式是之前所使用过的，而这个时候三个对象进行的内存分配的图形如下：

![](https://i.imgur.com/vvG43Qk.png)

既然现在描述的country都是中国，此时发现每一个对象的country属性被重复保存。

	public class TestDemo {
		public static void main(String args[]) {
			Person p1 = new Person("张三", 10);
			Person p2 = new Person("李四", 11);
			Person p3 = new Person("王五", 12);
			p1.country = "中国民国";
			System.out.println(p1.getInfo());
			System.out.println(p2.getInfo());
			System.out.println(p3.getInfo());
		}
	}
**console：**

	姓名： 张三, 年龄 ：10, 国家： 中国民国
	姓名： 李四, 年龄 ：11, 国家： 中国
	姓名： 王五, 年龄 ：12, 国家： 中国

传统属性具备的特征就是保存在堆内存之中，并且每一个对象独享此属性，可是同样的概念明显不适合于批量改变同一属性的内容，最好的做法就是将country属性变为共享属性，只要一次修改就可以影响所有对象。如果要描述共享属性只要在属性前追加static关键字。

**范例** 定义static 共享属性：

	class Person {
		private String  name;
		private int age;
		static String country = "中国";   //为了后面的操作放笔恩，暂时不封装
		public Person(String name, int age) {
			this.name = name;
			this.age = age;
		}
		
		public String getInfo() {
			return "姓名： " + this.name + ", 年龄 ：" + this.age + ", 国家： " + this.country ;
		}
	}
	
	public class TestDemo {
		public static void main(String args[]) {
			Person p1 = new Person("张三", 10);
			Person p2 = new Person("李四", 11);
			Person p3 = new Person("王五", 12);
			p1.country = "中国民国";
			System.out.println(p1.getInfo());
			System.out.println(p2.getInfo());
			System.out.println(p3.getInfo());
		}
	}

**console：**

	姓名： 张三, 年龄 ：10, 国家： 中国民国
	姓名： 李四, 年龄 ：11, 国家： 中国民国
	姓名： 王五, 年龄 ：12, 国家： 中国民国

当程序中使用static关键字进行定义后，此属性将不保存在堆内存中，会保存在全局数据区的内存空间中，并且所有的对象都可以进行该数据区的访问。

![](https://i.imgur.com/GP0x958.png)

但是现在既然使用的是共享属性，代码就会出现一个问题，共享属性能通过一个对象修改吗？
对于static属性也会将其称为类属性，而所有的类属性都可以利用类名称直接调用。

	Person.country = "中国民国";

结论：访问static属性都使用类名称，使用对象名称访问属于不规范操作

所有非static的属性必须在产生实例化对象之后才可以使用，而所有static属性不受实例化对象的限制，是否有对象与static属性操作无关。

	public class TestDemo {
		public static void main(String args[]) {
			System.out.println(Person.country);
			//static属性能够直接通过类名称调用
			Person.country = "中国民国";
			System.out.println(Person.country);
		}
	}

**console：**

	中国
	中国民国

选择： 关于static属性与非static属性定义的选择

- 在定义类99%的情况下是不会考虑static属性的；

- 如果需要描述共享属性的概念或者不希望受到实例化对象控制的时候使用static属性；



## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course44)
