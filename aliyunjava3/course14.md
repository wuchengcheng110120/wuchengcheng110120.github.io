## [上一页](course13)
## 枚举（Enum类）

严格来讲虽然JDK1.5提供有enum关键字，但是enum并不是一种新的结构，相反，它只是对一种类型的包装：使用关键字enum定义的枚举类本质上就相当于一个class定义的类继承了java.lang.Enum父类。

在Enum里面有以下的方法：

- 构造方法：protected Enum(String name,int ordinal)

	|-当定义枚举类中对象的时候自动设置序号和名字；

- 取得枚举名字：public final String name()

- 取得枚举序号：public final int ordinal()

**范例** 观察方法的使用：

	package cn.mldn.demo;
	
	enum Color {
		RED,GREEN,BLUE;
	}
	
	public class TestDemo {
		public static void main(String[] args) {
			System.out.println(Color.RED.ordinal()+ " = " + Color.RED.name());
		}
	}

**console：**

	0 = RED

在枚举类中还有一个方法可以取得所有的枚举数据：values（）返回的是一个枚举对象的数组

**范例** 取得所有的枚举数据：

	package cn.mldn.demo;
	
	enum Color {
		RED,GREEN,BLUE;
	}
	
	public class TestDemo {
		public static void main(String[] args) {
			for(Color temp: Color.values()) {
				System.out.println(temp.ordinal()+ " = " + temp.RED.name());
			}
		}
	}

**console：**

	0 = RED
	1 = RED
	2 = RED

请解释enum和Enum的区别？

- enum是一个关键字，使用enum定义的枚举类本质上就相当于一个类继承了Enum这个抽象类而已；







## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course15)
