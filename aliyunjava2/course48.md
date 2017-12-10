## [上一页](course47)

##  代码块（构造块）

构造块指的是定义在类中的代码块。

**范例** 定义构造块：

	class Person{
		{
			System.out.println("1 、 Person类的构造块");
		}
		public Person(){
			System.out.println("2 、 Person类的构造方法");
		}
	}
	
	public class TestDemo {
		public static void main(String args[]) {
			new Person();
			new Person();
		}
	}

每一次使用关键字new实例化对象的时候一定会调用构造方法，但是有了构造块之后发现构造块会优先于构造方法先执行。

这个构造块唯一的作用是可以进行简单的逻辑操作，但是有没有什么用。

	class Person{
		private String info = "hello";
		{//在构造块中先进行一些处理
			for (int i = 0; i < 10; i++) {
				info += i;
			}
		}
		public Person(){
			System.out.println("2 、 Person类的构造方法" + info);
		}
	}
	
	public class TestDemo {
		public static void main(String args[]) {
			new Person();
			new Person();
		}
	}

构造块的使用是一种补充手段，而这种手段并没有太大的意义。

## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course49)
