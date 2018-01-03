## [上一页](course25)
## Java多线程实现（Thread类实现多线程）

想要实现多线程，那么必须有一个前提：有一个线程执行主类。

![](http://ww3.sinaimg.cn/large/0060lm7Tly1fn3aa3z281j30uf0gx79p.jpg)

如果现在要想实现一个多线程的主类，有两类途径：

- 继承一个Thread类；

- 【推荐】实现Runnable、Callable接口；

java.lang.Thread 是一个线程操作的核心类。如果现在想要定义一个线程的主类，那么最简单的方法就是直接继承Thread类，而后覆写该类中的run（）方法（相当于线程的主方法）。

**范例** 线程主体类：

	package cn.mldn.demo;
	
	class MyThread extends Thread{//是一个线程的主体类
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
	
	public class TestDemo {
		public static void main(String[] args) {
			
		}
	}

当现在有了线程的主体类之后，很明显首先就一定会想到产生对象随后调用方法，但是你现在不能够直接调用run（）方法。

**范例** 观察直接调用run（）方法：

	public class TestDemo {
		public static void main(String[] args) {
			MyThread mt1 = new MyThread("线程A");
			MyThread mt2 = new MyThread("线程B");
			MyThread mt3 = new MyThread("线程C");
			mt1.run();
			mt2.run();
			mt3.run();
		}
	}
**console：**

	线程A, i = 0
	线程A, i = 1
	线程A, i = 2
	线程A, i = 3
	线程A, i = 4
	线程A, i = 5
	线程A, i = 6
	线程A, i = 7
	线程A, i = 8
	线程A, i = 9
	线程B, i = 0
	线程B, i = 1
	线程B, i = 2
	线程B, i = 3
	线程B, i = 4
	线程B, i = 5
	线程B, i = 6
	线程B, i = 7
	线程B, i = 8
	线程B, i = 9
	线程C, i = 0
	线程C, i = 1
	线程C, i = 2
	线程C, i = 3
	线程C, i = 4
	线程C, i = 5
	线程C, i = 6
	线程C, i = 7
	线程C, i = 8
	线程C, i = 9

这个时候只是做了一个顺序打印，与多线程没有关系，多线程的执行实际上和进程是相似的，也应该采用多个程序交替执行，而不是各自执行各自的。正确启动多线程的方式应该调用的是Thread类中的start（）方法。

- 启动多线程：public void start()，调用此方法会调用run（）

**范例** 正确的启动多线程：

	public class TestDemo {
		public static void main(String[] args) {
			MyThread mt1 = new MyThread("线程A");
			MyThread mt2 = new MyThread("线程B");
			MyThread mt3 = new MyThread("线程C");
			mt1.start();
			mt2.start();
			mt3.start();
		}
	}

**console：**

	线程B, i = 0
	线程A, i = 0
	线程C, i = 0
	线程C, i = 1
	线程C, i = 2
	线程C, i = 3
	线程C, i = 4
	线程C, i = 5
	线程C, i = 6
	线程C, i = 7
	线程C, i = 8
	线程C, i = 9
	线程A, i = 1
	线程A, i = 2
	线程A, i = 3
	线程A, i = 4
	线程A, i = 5
	线程A, i = 6
	线程A, i = 7
	线程A, i = 8
	线程B, i = 1
	线程A, i = 9
	线程B, i = 2
	线程B, i = 3
	线程B, i = 4
	线程B, i = 5
	线程B, i = 6
	线程B, i = 7
	线程B, i = 8
	线程B, i = 9

再次执行代码发现所有的线程对象变为了交替执行。

疑问：为什么要通过start（）方法来调用run（）方法，而不是run（）直接执行？

- 如果想要解决此类问题，就必须打开Java源代码进行查看（在JDK安装目录下src.zip）；

	public synchronized void start() {
	        if (threadStatus != 0)
	            throw new IllegalThreadStateException();
	        group.add(this);
	
	        boolean started = false;
	        try {
	            start0();
	            started = true;
	        } finally {
	            try {
	                if (!started) {
	                    group.threadStartFailed(this);
	                }
	          	} catch (Throwable ignore) {
	          	  }
	       	  }
	 	   }
    private native void start0();

首先在本程序中发现该方法会抛出一个异常“IllegalThreadStateException”，如果按照原本的处理方式，这个时候在start（）方法上应该使用throws声明，或者直接在方法中进行try...catch处理，而此处不需要处理，所以它是一个RuntimeException的子类。这个异常的产生只是在你重复启动了多线程才会抛出。每一个线程对象只能启动一次。

可以看到在start（）方法中调用了一次start0（）方法，而这个方法是一个只声明而未实现的方法，同时使用了native关键字进行定义，native指的是调用本机的原生系统函数。

![](http://ww3.sinaimg.cn/large/0060lm7Tly1fn3ghkieusj30u70gqjxj.jpg)





## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course27)
