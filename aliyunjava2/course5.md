## [上一页](course4)


### 2.4 类与对象（引用传递初次分析） ###

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

**console**：

	name = 狗剩、age = 30


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

**console**：
	
	name = 狗剩、age = 30

观察此时的内存分析图：

![](https://i.imgur.com/3y7tRhc.png)


在程序开发过程中，所谓的垃圾空间就是指
> 没有任何栈内存指向的堆内存空间

所有的垃圾空间将被JAVA中的垃圾收集器（GC,garbage collector）进行回收，以实现内存空间的释放，不过从实际开发来讲，虽然JAVA提供有GC，但是GC也会造成程序性能的下降，所以程序开发过程中一定要控制好你的对象的产生数量，即：无用的对象尽可能少产生。

------

## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course6)
