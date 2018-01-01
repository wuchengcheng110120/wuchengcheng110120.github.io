## [上一页](course18)
## Annotation（过期声明）

@Deprecated

如果现在有一个程序类，从项目的1.0版本到项目的77.0版本一直都在使用，但是从78.0版本之后该配置可能会产生问题，那么这个时候不能直接删除这个类，因为其他旧版本可能还在使用这个类，并且这个类在旧版本中没有任何问题。所以这个时候就希望在进行新版本扩展的时候不要在使用这个不建议使用的类，所以加一个过期的注解。

**范例** 观察过期操作：

	package cn.mldn.demo;
	
	class Person {
		@Deprecated 	//表示该方法已经不建议使用了，但是即使使用了也不会出错
		public Person() {}
		public Person(String name) {}
		@Deprecated
		public void fun() {}
	}
	public class TestDemo {
		public static void main(String[] args) {
			Person per = new Person();//明确的标记出已过期
			per.fun();
			per = new Person(" ");
		}
	}

这种过期操作往往会出现在一些平台支持的工具上，例如: JDK就是一个平台，所以在JDK中许多的方法都不建议用户再继续使用了。

	String(byte[] ascii, int hibyte)
	Deprecated. 
	This method does not properly convert bytes into characters. As of JDK 1.1, the preferred way to do this is via the String constructors that take a Charset, charset name, or that use the platform's default charset.



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course20)
