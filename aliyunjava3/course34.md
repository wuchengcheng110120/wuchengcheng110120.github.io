## [上一页](course33)
## 线程的同步与死锁（同步问题引出）

线程的同步与死锁是整个多线程里面最需要重点理解的概念。这种操作的核心问题在于：每一个线程对象操作的延迟或者说轮番抢占资源的问题。

现在希望做一个简单的程序，希望其可以实现多个线程卖票的处理。所以初期的实现如下：

	package cn.mldn.demo;
	
	class MyThread implements Runnable{
		private int ticket = 10;//一共要卖的票的总数
		@Override
		public void run() {
			for(int x = 0; x < 20; x++) {
				if(this.ticket > 0) {
					System.out.println(Thread.currentThread().getName()
							+ "卖票， ticket =  " + this.ticket--);
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
	票贩子A卖票， ticket =  7
	票贩子A卖票， ticket =  6
	票贩子C卖票， ticket =  8
	票贩子B卖票， ticket =  9
	票贩子C卖票， ticket =  4
	票贩子A卖票， ticket =  5
	票贩子C卖票， ticket =  2
	票贩子B卖票， ticket =  3
	票贩子A卖票， ticket =  1

设置延迟：

	package cn.mldn.demo;
	
	class MyThread implements Runnable{
		private int ticket = 10;//一共要卖的票的总数
		@Override
		public void run() {
			for(int x = 0; x < 20; x++) {
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
	
	public class TestDemo {
		public static void main(String[] args)  {
			MyThread mt = new MyThread();
			new Thread(mt,"票贩子A").start();
			new Thread(mt,"票贩子B").start();
			new Thread(mt,"票贩子C").start();
		}
	}
**console：**

	票贩子B卖票， ticket =  10
	票贩子A卖票， ticket =  9
	票贩子C卖票， ticket =  10
	票贩子C卖票， ticket =  8
	票贩子A卖票， ticket =  7
	票贩子B卖票， ticket =  6
	票贩子C卖票， ticket =  5
	票贩子B卖票， ticket =  4
	票贩子A卖票， ticket =  3
	票贩子C卖票， ticket =  2
	票贩子B卖票， ticket =  1
	票贩子A卖票， ticket =  0
	票贩子C卖票， ticket =  -1

这个时候发现程序执行有错误，票数出现负数，这种操作就称为不同步操作。

![](http://ww2.sinaimg.cn/large/0060lm7Tly1fn4pkpfrn7j30vc0hhgts.jpg)

ticket =1 时三个线程进入判断，判断后延迟，导致出现ticket负数。

不同步的唯一好处是处理速度快（多个线程并发执行）。




## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course35)
