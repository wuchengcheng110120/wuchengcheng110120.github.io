## [上一页](course45)

##  static关键字（static应用）

static属性的最大功效是共享操作，所以在这一基础上可以使用static做一个对象产生的计数统计。所有新对象的产生都要使用构造方法完成，所以可以在构造方法中实现。

**范例** 对象产生个数：

	class Person{
		private static int count = 0;//保存对象产生个数
		public Person() {
			System.out.println("对象个数： " + ++count);
		}
	}
	
	public class TestDemo {
		public static void main(String args[]) {
			new Person();
			new Person();
			new Person();
		}
	}

**console：**

	对象个数： 1
	对象个数： 2
	对象个数： 3

在以上代码的基础上做一个简单的扩充，假设Person类中有一个name属性以及两个构造方法，其中一个构造方法可以接受外部传递的name属性内容，而另外一个构造方法是无参构造，一旦使用无参构造就希望可以自动的为类中的name属性赋值，例如“NONAME-1”。那么此时就可以继续使用static属性控制。

	class Person{
		private String name;
		private static int count = 0;//保存对象产生个数
		public Person() {//需要由程序自己来设置内容
			this("NONAME - " + count ++);//调用本类有参构造
		}
		public Person(String name) {//由外部传递属性内容
			this.name = name; 
		}
		public String getName() {
			return this.name;
		}
	}
	
	public class TestDemo {
		public static void main(String args[]) {
			System.out.println(new Person().getName());
			System.out.println(new Person("MLDN").getName());
			System.out.println(new Person().getName());
		}
	}

以后也会见到这种自动为属性命名的操作。

1、 static定义的属性和方法并不是你在进行类设计时的首要选择；

2、 static的属性和方法不受到一个类的实例化对象限制

## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course47)
