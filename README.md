## Welcome to wuchengcheng's GitHub Pages


**尽量避免问题，遇到问题，解决问题**
--------

# JAVA 学习 #
## 20171118 阿里云课程面向对象day1 ##

----------

## 1面向对象简介 ##

	OOA(面向对象分析),OOD（面向对象设计）,OOP（面向对象编程）

封装、继承、多态

类共性特征，个性特征

对象的特征在类实际开发过程中进行完整定义

类中的组成：属性（变量，描述每一个对象的具体特点）、方法（操作的行为）

----------
## 2类与对象 ##
### 2.1类与对象（类与对象的基本定义） ###

class 类名 {
	
	属性；
	属性；
	方法（）{
	    }
		
}

类定义完之后是不能够直接去使用的，想要使用类那么必须产生对象
	
    而对象的定义分为以下两种语法形式：
 	
	声明并实例化对象： 类名称 对象名称 = new 类名称（）；
	分步进行对象实例化：
		声明对象：类名称 对象名称 = null
		实例化对象：对象名称 = new 类名称

引用数据类型的最大特征在于内存的分配 而只要出现有关键字new，那么就只有一个解释 ：new 开辟内存

内存是不可能无线开辟的，所以这个时候所谓的性能调优调整的就是内存问题

## 20171119 阿里云课程面向对象day2 ##

### 2.2类与对象（类与对象定义） ###

所有的对象只有实例化之后才可以真正使用，而对象的使用都是围绕着类来进行的那么此时使用就有两种形式：
	
- 调用类中的属性： 对象.属性 = 内容；
- 调用类中的方法： 对象.方法（）；

		class Person{
		
			String name;
			int age;
			public void info() {
				System.out.println("name = "+ name + "、age = "+  age);
			}
		}

		public class TestDemo {
	
			public static void main(String[] args) {
				// TODO Auto-generated method stub
				//类名称 对象名称 = new 类名称（）；
				Person person = new Person();
				person.name = "张三";//设置对象中的属性
				person.age = 25;//设置对象中的属性
				person.info();//调用类中的方法
						
			}
		}


----------
### 2.3类与对象（对象的内存分析） ###

如果想对对象进行产生分析，那么就必须清楚引用类型。

引用类型指的是内存空间的操作。所谓的引用类型就是获得储存空间。

而对于现在的内存，主要要会使用两块内存空间：

- 堆内存空间：保存真正的数据,堆内存保存的是对象的属性信息；
- 栈内存空间：保存的堆内存的地址，堆内存的操作权，如果想要简化理解，可以理解为保存的是对象名称；

		public class TestDemo {
		
			public static void main(String[] args) {
				// TODO Auto-generated method stub
				//类名称 对象名称 = new 类名称（）；
				Person person = new Person();
				
				person.info();//调用类中的方法
						
			}
		}

**<font size=5>console</font>**：name = null、age = 0 

string初始化为null，int初始化为0

所以按照之前的程序，那么现在就给出如下的内存参考图：
![](https://i.imgur.com/OFOD6vQ.png)

但是对于对象的产生实际上要知道一共会有两种格式，现在使用的是声明并实例化对象的格式，那么也可以分步的方式完成。

		public class TestDemo {
		
			public static void main(String[] args) {
				
				Person person = null;
				person = new Person();
				person.info();//调用类中的方法
						
			}
		}

内存参考图：

![](https://i.imgur.com/wmFqEBh.png)

但是千万要记住一点，对象（所有的引用数据类型），必须在其开辟空间之后才可以使用。

如果使用了未开辟内存空间的引用数据类型，则将出现NullPointerException：

		public class TestDemo {
		
			public static void main(String[] args) {
				Person person = null;
				person.info();//调用类中的方法
						
			}		
		}


这个时候只声明了对象，而没有为其开辟堆内存空间，而本程序在编译的时候不会产生任何的语法错误，在执行的时候会出现如下的错误提示：

		Exception in thread "main" java.lang.NullPointerException
			at bznoc171118.TestDemo.main(TestDemo.java:20)

“NullPointerException”是在整个开发人生中陪伴你到最后的的异常，只有引用数据类型（数组、类、接口）才会出现此类异常，以后出现此类错误，根据出现错误的位置查看是否实例化。


### 2.4类与对象（引用传递初次分析） ###

所有初学者最难的部分就是引用传递的分析。

以后的开发之中都是引用传递。

引用传递的本质就在于别名，而这个别名只不过是放在了栈内存之中，一个对内存可以被多个栈内存引用。

**范例** 观察引用传递1：

		class Person{
			String name;
			int age;
			public void info() {
				System.out.println("name = "+ name + "、age = "+  age);
			}
		}
		public class TestDemo {
		
			public static void main(String[] args) {
				Person per1 = new Person();
				per1.name = "小于子";
				per1.age = 30;
				//此步骤就是内存传递
				Person per2 = per1;//采用同样的类型接收
				per2.name = "狗剩";//设置一个名字
				per1.info();
			}
		}

**<font size=5>console</font>**：name = 狗剩、age = 30


内存参考图：

![](https://i.imgur.com/lmK9ckU.png)

**范例** 观察引用传递2：

		class Person{
			String name;
			int age;
			public void info() {
				System.out.println("name = "+ name + "、age = "+  age);
			}
		}
		public class TestDemo {
		
			public static void main(String[] args) {
				Person per1 = new Person();
				Person per2 = new Person();
				per1.name = "小于子";
				per1.age = 30;
				per2.name = "张三";
				per2.age = 20;
				//此步骤就是内存传递
				per2 = per1;//采用同样的类型接收
				per2.name = "狗剩";//设置一个名字
				per1.info();
			}
		}

**<font size=5>console</font>**：name = 狗剩、age = 30

观察此时的内存分析图：

![](https://i.imgur.com/3y7tRhc.png)


在程序开发过程中，所谓的垃圾空间就是指没有任何栈内存指向的堆内存空间，所有的垃圾空间将被JAVA中的垃圾收集器（GC,garbage collector）进行回收，以实现内存空间的释放，不过从实际开发来讲，虽然JAVA提供有GC，但是GC也会造成程序性能的下降，所以程序开发过程中一定要控制好你的对象的产生数量，即：无用的对象尽可能少产生。

------
## 3利用private实现封装 ##
面向对象三大特征：封装、继承、多态

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
**<font size=5>console</font>**：name = 张三、age = 0


无论是否使用setter（）和getter（）都要提供。

如果现在非要进行检测要在setter（）中进行。

**<font size=5>类的设计原则：</font>**

以后在编写类的时候类中的所有属性必须使用***private*** 封装。

而使用***private*** 封装的属性如果需要被外部类使用，那么就按照格式定义相应的setter（）和getter（）方法。

private实现封装的最大特征在于：只允许本类访问而不允许其他类访问。

private只是封装的第一步，学习private为了学习基本程序逻辑，封装还要结合继承和多态。








