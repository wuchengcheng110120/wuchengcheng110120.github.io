## 3 利用private实现封装 ##


> 面向对象三大特征：封装、继承、多态

封装是整个JAVA中最复杂的概念，本次讲解是封装的基本概念。

如果想要清楚封装，先要知道没有封装会怎么样。

**范例** 
	class Person{
		String name;
		int age;
		public void info() {
			System.out.println("name = "+ name + "、age = "+  age);
		}
	}

	public class TestDemo {
		
		public static void main(String[] args) {
			Person per = new Person();
			per.name = "张三";
			per.age = -200;
			per.info();
		}
	}

这个时候不会出现任何语法错误，因为从int型的数据保存范围来讲，允许有负数，但不会有年龄为-200，那么也就证明这个时候属于业务逻辑错误。

此时如果想要回避此类问题，那么首先要解决的就是如何可以让对象不能够直接操作年龄的属性，或者指的是，外部操作如何不能够直接操作类中的敏感内容。所以此事解决问题的核心观念，如何让内部操作对外部不可见，此时就可以使用***private***关键字来实现。

**范例** 利用private来实现封装：

	class Person{
		private String name;
		private int age;
		public void info() {
			System.out.println("name = "+ name + "、age = "+  age);
		}
	}
	public class TestDemo {
		
		public static void main(String[] args) {
			Person per = new Person();
		//	per.name = "张三";
		//	per.age = -200;
			per.info();
		}
	}


类中的属性和方法都可以使用***private*** 来定义，但大部分情况下很少会在方法上使用***private***。

一旦属性的声明上使用了***private***定义之后，那么其他类直接进行该属性访问时就会出现错误。

使用private声明之后属性安全了，外部无法直接操作了，但是新的问题出现了，如果想要进行***private*** 私有属性的访问，按照java的设计原则就需要使用***setter（）*** 和***getter（）*** 方法：

- setter方法：主要用于属性内容的设置；
   
	private String name：public void setName(String n);

- setter方法：主要用于属性内容的取得；
     
	private String name：public void setName(String n);

**范例** 扩展Person类中的内容：

	class Person{
		private String name;
		private int age;
		public void setName(String n) {
			name = n;
		}
		public void setAge(int a) {
			if(a >= 0 && a<= 250) {
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
		public void info() {
			System.out.println("name = "+ name + "、age = "+  age);
		}
	}

	public class TestDemo {
		
		public static void main(String[] args) {
			Person per = new Person();
			per.setName("张三");
			per.setAge(-200);
			per.info();
		}
	}	
**console**：

    name = 张三、age = 0


无论是否使用setter（）和getter（）都要提供。

如果现在非要进行检测要在setter（）中进行。

***类的设计原则：***

以后在编写类的时候类中的所有属性必须使用***private*** 封装。

而使用***private*** 封装的属性如果需要被外部类使用，那么就按照格式定义相应的setter（）和getter（）方法。

private实现封装的最大特征在于：
> 只允许本类访问而不允许其他类访问。

private只是封装的第一步，学习private为了学习基本程序逻辑，封装还要结合继承和多态。



## [back to the list](learnJava)
## [next page](course7)
