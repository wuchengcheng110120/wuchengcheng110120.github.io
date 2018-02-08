## [上一页](course112)
##   反射与Annotation（自定义Annotation）

如果想要自定义Annotation，首先要解决的是Annotation的作用范围，通过之前的取得可以发现，不同的Annotation一定有自己的运行范围，而这些范围就在一个枚举类（java.lang.annotation.RetentionPolicy）中定义：

- public static final RetentionPolicy SOURCE：在源代码中出现的Annotation

- public static final RetentionPolicy CLASS ： 类定义的时候出现的Annotation

- public static final RetentionPolicy RUNTIME ： 类执行时候出现的Annotation

**范例** 定义一个在运行时生效的Annotation：

	package cn.mldn.demo;
	
	import java.io.Serializable;
	import java.lang.annotation.Annotation;
	import java.lang.annotation.Retention;
	import java.lang.annotation.RetentionPolicy;
	
	@Retention(RetentionPolicy.RUNTIME) // 表示此Annotataion在运行时生效
	@interface MyAnnotation{//定义了一个自己的Annotation
		public String name(); // 表示定义了一个属性
		public int age();
	}
	
	@SuppressWarnings("serial")
	@MyAnnotation(age = 10, name = "mldn")
	class Member implements Serializable{}
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			Annotation ant[] =  Member.class.getAnnotations();
			for (int x = 0; x < ant.length; x++) {
				System.out.println(ant[x]);
			}
		} 	
	}
**console：**

	@cn.mldn.demo.MyAnnotation(age=10, name=mldn)

此时要求强制设置属性的name和age属性内容，这样很不方便，希望可以使用默认值，所以在Annotation定义的时候用default来设置默认值：

	package cn.mldn.demo;
	
	import java.io.Serializable;
	import java.lang.annotation.Annotation;
	import java.lang.annotation.Retention;
	import java.lang.annotation.RetentionPolicy;
	
	@Retention(RetentionPolicy.RUNTIME) // 表示此Annotataion在运行时生效
	@interface MyAnnotation{//定义了一个自己的Annotation
		public String name()default "mldnjava"; // 表示定义了一个属性
		public int age()default 11;
	}
	
	@SuppressWarnings("serial")
	@MyAnnotation
	class Member implements Serializable{}
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			Annotation ant[] =  Member.class.getAnnotations();
			for (int x = 0; x < ant.length; x++) {
				System.out.println(ant[x]);
			}
		} 	
	}
**console：**

	@cn.mldn.demo.MyAnnotation(name=mldnjava, age=11)

之前的操作都是取得全部Annotation的信息，现在也可以取得某个具体的Annotation。

**范例** 取得某个具体的Annotation：

	package cn.mldn.demo;
	
	import java.io.Serializable;
	import java.lang.annotation.Annotation;
	import java.lang.annotation.Retention;
	import java.lang.annotation.RetentionPolicy;
	
	@Retention(RetentionPolicy.RUNTIME) // 表示此Annotataion在运行时生效
	@interface MyAnnotation{//定义了一个自己的Annotation
		public String name()default "mldnjava"; // 表示定义了一个属性
		public int age()default 11;
	}
	
	@SuppressWarnings("serial")
	@MyAnnotation
	class Member implements Serializable{}
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			MyAnnotation ant =  Member.class.getAnnotation(MyAnnotation.class);
			System.out.println("姓名： " + ant.name() + "，年龄： " + ant.age());
		} 	
	}

**console：**

	姓名： mldnjava，年龄： 11

可以在Annotation中编写许多属性信息，也可以定义许多有意义的Annotation，但是请记住：Annotation的使用需要特殊环境，不是随意编写的。


## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course114)
