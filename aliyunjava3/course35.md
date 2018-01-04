## [上一页](course34)
## 线程的同步与死锁（同步处理）

所谓的同步指的是所有的线程不是一起进入到方法中执行，而是按照顺序一个一个进来。

![](http://ww2.sinaimg.cn/large/0060lm7Tly1fn4ptqeavkj30vc0hhdpv.jpg)

如果想要实现“锁”的功能，那么可以采用synchronized关键字进行处理，有两种处理模式：同步代码块、同步方法。

1、 使用同步代码块

- 如果要使用同步代码块，必须设置一个要锁定的对象，所以一般可以锁定当前对象：this

	package cn.mldn.demo;
	
	class MyThread implements Runnable{
		private int ticket = 10;//一共要卖的票的总数
		@Override
		public void run() {
			for(int x = 0; x < 20; x++) {
				synchronized(this) {//在同一时刻，只允许一个线程进入并操作，其它线程需要等待
					//表示为程序逻辑上锁
					if(this.ticket > 0) {
						try {
							Thread.sleep(200);
						} catch (InterruptedException e) {
							e.printStackTrace();
						}
						System.out.println(Thread.currentThread().getName()
								+ "卖票， ticket =  " + this.ticket--);
					}
				}
				
			}
		}
	}
	
	public class TestDemo {
		public static void main(String[] args)  {
			MyThread mt = new MyThread();
			new Thread(mt,"票贩子A").start();
			new Thread(mt,"票贩子B").start();
			new Thread(mt,"票贩子C").start();
		}
	}
**console：**

	票贩子A卖票， ticket =  10
	票贩子A卖票， ticket =  9
	票贩子A卖票， ticket =  8
	票贩子A卖票， ticket =  7
	票贩子C卖票， ticket =  6
	票贩子B卖票， ticket =  5
	票贩子B卖票， ticket =  4
	票贩子B卖票， ticket =  3
	票贩子B卖票， ticket =  2
	票贩子C卖票， ticket =  1

第一种方式是在方法里拦截的，进入到run（）方法中的线程依然可能有很多个。

2、 同步方法

	package cn.mldn.demo;
	
	class MyThread implements Runnable{
		private int ticket = 10;//一共要卖的票的总数
		@Override
		public void run() {
			for(int x = 0; x < 20; x++) {
				this.sale();
			}
				
		}
		public synchronized void  sale() {
			if(this.ticket > 0) {
				try {
					Thread.sleep(200);
				} catch (InterruptedException e) {
					e.printStackTrace();
				}
				System.out.println(Thread.currentThread().getName()
						+ "卖票， ticket =  " + this.ticket--);
			}
		}
	}
	public class TestDemo {
		public static void main(String[] args)  {
			MyThread mt = new MyThread();
			new Thread(mt,"票贩子A").start();
			new Thread(mt,"票贩子B").start();
			new Thread(mt,"票贩子C").start();
		}
	}

同步虽然可以保证数据的完整性（线程安全操作），但是其执行速度会很慢。







## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course36)
