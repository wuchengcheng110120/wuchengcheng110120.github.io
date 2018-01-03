## [上一页](course26)
## Java多线程实现（Runnable接口实现多线程）

Thread类的功能是进行线程的启动，但如果一个类直接继承了Thread类所造成的问题就是单继承局限，那么在java中又提供有另外一种实现模式：Runnable接口。那么首先来观察一下此接口定义。

	@FunctionalInterface
	public interface Runnable{
	
		public void run()
	
	}

可以发现在接口里面同时存在有一个run（）方法，这一点和Thread是相同的，因为只要是接口的子类就必须覆写run（）方法。

**范例** 利用Runnable定义线程主体类：

	class MyThread implements Runnable{//是一个线程的主体类
		private String title;
		public MyThread(String title) {
			this.title = title;
		}
		@Override
		public void run() {//所有的线程从此处开始执行
			for (int i = 0; i < 10; i++) {
				System.out.println(this.title + ", i = " + i);
			}
		}
	}
但是新的问题出现了，此时MyThread类继承的不再是Thread类，而实现了Runnable接口，虽然解决了单继承，但是没有了Thread类的start（）方法被继承了。那么此时就需要关注Thread类提供的构造方法：

- 构造方法 public Thread(Runnable target)，可以接受Runnable接口对象；

**范例** 启动多线程：

	public class TestDemo {
		
		public static void main(String[] args) {
			MyThread mt1 = new MyThread("线程A");
			MyThread mt2 = new MyThread("线程B");
			MyThread mt3 = new MyThread("线程C");
			new Thread(mt1).start();
			new Thread(mt2).start();
			new Thread(mt3).start();
		}
	}

这个时候就启动了多线程，多线程的启动永远都是Thread类的start（）方法。

但是需要注意的是对于此时的Runnable接口对象也可以采用匿名内部类或Lambda表达式来进行定义。

**范例** 通过匿名内部类定义操作：

	package cn.mldn.demo;
	
	public class TestDemo {
		
		public static void main(String[] args) {
			new Thread(new Runnable() {
				@Override
				public void run() {
					System.out.println("hello world ! ");
				}
			}).start();
		}
	}

**范例** 使用Lambda表达式处理：

	package cn.mldn.demo;
	
	public class TestDemo {
		
		public static void main(String[] args) {
			new Thread(()->System.out.println("hello world !")).start();
		}
	}

在实际开发之中，Runnable接口的子类的定义形式可能很少出现，以上的这种操作是最为常见的做法。







## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course28)
