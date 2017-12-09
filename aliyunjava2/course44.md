## [上一页](course43)

##  static关键字（static 方法）


使用static定义的属性可以被类名称直接访问，那么同样使用static定义的方法也可以使用类名称直接访问，不用受实例化对象的控制。

**范例** 观察static定义的方法：

	class Person {
		private String  name;
		private int age;
		private static String country = "中国";   //为了后面的操作放笔恩，暂时不封装
		public Person(String name, int age) {
			this.name = name;
			this.age = age;
		}
		
		public static void setCountry(String c) {
			country = c; // 设置内容
		}
		public String getInfo() {
			return "姓名： " + this.name + ", 年龄 ：" + this.age + ", 国家： " + this.country ;
		}
	}
	
	public class TestDemo {
		public static void main(String args[]) {
			Person.setCountry("中华民国");// 没有实例化对象
			
			Person p1 = new Person("张三", 10);
			System.out.println(p1.getInfo());
			
		}
	}

**console：**

	姓名： 张三, 年龄 ：10, 国家： 中华民国

现在类中已经存在static方法和非static方法，对于两者的互相调用就存在有限制：

- 所有static方法不允许调用非static定义的属性或者方法；

- 所有的非static方法允许调用static属性或方法。

原因：因为所有的static方法允许在实例化之前进行访问，而所有非static操作必须在实例化对象产生之后才可以操作。

使用static属性是共享目的（因为属性都需要封装），但是使用static方法的目的只有一个：某些方法不希望受到类的限制，可以在没有实例化对象的时候进行执行。

## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course45)
