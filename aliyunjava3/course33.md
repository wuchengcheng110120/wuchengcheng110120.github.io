## [上一页](course32)
## 多线程常用操作方法（线程优先级）

所谓的线程优先级值得是线程优先级越高越有可能先执行，但仅仅是有可能而已，在Thread类中提供有以下的优先级操作方法。

- 设置优先级：public final void setPriority(int newPriority)

- 取得优先级：public final int getPriority()

对于优先级设置的内容可以通过Thread类的几个常量来决定：

- 最高优先级：public static final int MAX_PRIORITY 10

- 中等优先级：public static final int NORM_PRIORITY 5

- 最低优先级：public static final int MIN_PRIORITY 1

**范例** 设置优先级：

	package cn.mldn.demo;
	
	class MyThread implements Runnable{
		@Override
		public void run() {
			for(int x = 0; x < 2; x++) {
				System.out.println(Thread.currentThread().getName()
						+ ", x = " + x);
			}
		}
	}
	
	public class TestDemo {
		public static void main(String[] args)  {
			MyThread mt = new MyThread();
			Thread t1 = new Thread(mt,"线程A");
			Thread t2 = new Thread(mt,"线程B");
			Thread t3 = new Thread(mt,"线程C");
			t1.setPriority(Thread.MIN_PRIORITY);
			t2.setPriority(Thread.MAX_PRIORITY);
			t3.setPriority(Thread.NORM_PRIORITY);
			t1.start();
			t2.start();
			t3.start();
		}
	}

那么主方法是一个线程，主方法的优先级是多少呢？

	public class TestDemo {
		public static void main(String[] args)  {
			System.out.println(Thread.currentThread().getPriority());
		}
	}
**console：** 

	5	

主方法只是一个中等优先级。



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course34)
