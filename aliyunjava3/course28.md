## [上一页](course27)
## Java多线程实现（Thread与Runnable区别）

首先从实现形式上使用Runnable接口实现多线程会更好，因为避免了单继承局限，但是除了这点之外，实际上Thread与Runnable之间也存在着一些联系。首先观察一下Thread类的继承定义形式：

public class Thread
extends Object
implements Runnable

原来Thread类是Runnable接口的实现子类：那么Thread类也应该覆写了run（）方法。

	@Override
    public void run() {
        if (target != null) {
            target.run();
       }
	}

 	public Thread(Runnable target) {
        init(null, target, "Thread-" + nextThreadNum(), 0);
    }


	private void init(ThreadGroup g, Runnable target, String name,
                      long stackSize) {
        init(g, target, name, stackSize, null, true);
    }

	private Runnable target;

结合之前的程序代码就可以形成如下的类继承结构：

![](http://ww3.sinaimg.cn/large/0060lm7Tly1fn3h34jsigj30uf0gvgr5.jpg)

所以在多线程的处理上使用的就是代理设计模式。除了以上的关系之外，实际上在开发中使用Runnable还有一个特点，使用Runnable实现的多线程的程序类可以更好的描述出数据共享的概念（并不是说Thread不能）。

目标是希望产生若干个线程进行同一数据的处理操作。

**范例** 使用Thread实现数据操作

	package cn.mldn.demo;
	class MyThread extends Thread{//是一个线程的主体类
		private int ticket =10;//一共10张票
		@Override
		public void run() {
			for (int i = 0; i < 10; i++) {
				if (this.ticket > 0 ) {
					System.out.println("卖票， ticket = " + this.ticket--);
				}
			}
		}
	}
	
	public class TestDemo {
		
		public static void main(String[] args) {
			new MyThread().start();
			new MyThread().start();
			new MyThread().start();
		}
	}

此时只是想启动三个线程进行卖票处理。结果变为了各自卖各自的票。
	
	public class TestDemo {
		
		public static void main(String[] args) {
			MyThread mt = new MyThread();
			new Thread(mt).start();
			new Thread(mt).start();
			new Thread(mt).start();
		}
	}

MyThread有start（）方法还要去使用Thread类的start方法。

**范例** 使用Runnable实现共享：

	package cn.mldn.demo;
	class MyThread implements Runnable{//是一个线程的主体类
		private int ticket =10;//一共10张票
		@Override
		public void run() {
			for (int i = 0; i < 10; i++) {
				if (this.ticket > 0 ) {
					System.out.println("卖票， ticket = " + this.ticket--);
				}
			}
		}
	}
	
	public class TestDemo {
		
		public static void main(String[] args) {
			MyThread mt = new MyThread();
			new Thread(mt).start();
			new Thread(mt).start();
			new Thread(mt).start();
		}
	}

![](http://ww3.sinaimg.cn/large/0060lm7Tly1fn3j08abwmj30u90gqgqw.jpg)

使用Runnable有更好的实现数据共享的多线程操作。



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course29)
