## [上一页](course22)
## 方法引用

最初开始的引用都是针对于引用类型完成的，也就是说只有数组、类、接口具备引用的操作，但是现在开始，追加了方法引用的概念。实际上引用的本质就是别名。所以方法的引用也是别名的使用，而方法引用的类型可以由四种形式：

- 引用静态方法： 类名称 ：：static 方法名称

- 引用某个对象的方法： 实例化对象：：普通方法

- 引用某个特定类的方法： 类名称：：普通方法

- 引用构造方法： 类名称：：new


**范例** 引用静态方法：

- 在String 类中有一个valueOf（）方法，这个方法就是进行静态调用的

	package cn.mldn.demo;
	
	interface IUtil<P,R>{
		public R zhuanhuan(P p);
	}
	
	public class TestDemo {
		public static void main(String[] args) {
			IUtil<Integer,String> iu = String :: valueOf;//进行方法引用
			String str = iu.zhuanhuan(1000);//相当于 String.valueOf（1000）
			System.out.println(str.length());
		}
	}

就相当于为方法起了个别名。

**范例** 引用某个对象中的方法：

	package cn.mldn.demo;
	
	interface IUtil<R>{
		public R zhuanhuan();
	}
	
	public class TestDemo {
		public static void main(String[] args) {
			IUtil<String> iu = "hello" :: toUpperCase;//进行方法引用
			System.out.println(iu.zhuanhuan());//相当于转换的是“hello”
		}
	}


**范例** 引用类中的普通方法：

- String类中有一个compareTo（），进行比较大小；

	package cn.mldn.demo;
	
	interface IUtil<R,P>{
		public R 比较(P p1,P p2);
	}
	
	public class TestDemo {
		public static void main(String[] args) {
			IUtil<Integer,String> iu = String::compareTo;//进行方法引用
			System.out.println(iu.比较("H", "h"));//相当于转换的是“hello”
		}
	}

**范例** 引用构造方法：

	package cn.mldn.demo;
	
	class Person{
		private String name;
		private int age;
		public Person(String name, int age) {
			this.name = name;
			this.age = age;
		}
		@Override
		public String toString() {
			return "Person [name=" + name + ", age=" + age + "]";
		}
	}
	@FunctionalInterface
	interface IUtil<R,FP,SP>{
		public R creat(FP p1, SP p2);
	}
	
	public class TestDemo {
		public static void main(String[] args) {
			IUtil<Person,String,Integer> iu = Person :: new;
			System.out.println(iu.creat("张三", 20));
		}
	}

这些都属于Lambda的补充。





## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course24)
