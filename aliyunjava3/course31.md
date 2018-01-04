
## [上一页](course30)
## 多线程常用操作方法（线程命名和取得）

所有多线程的操作方法都在Thread类里面，也就是说所谓的方法就是一个查询文档的过程。由于现在的开发过程中很少会直接出现多线程的编写代码，对于此部分重点掌握核心的几个方法就行了。

多线程的运行状态是不确定的，所以对于多线程的操作必须有一个可以明确标示出线程对象的信息，而这个信息往往就使用名称来描述，那么在Thread类里面提供有如下的线程的名称操作方法：

1、 public Thread(Runnable target,String name)，构造，创建线程对象的时候设置好名字

2、 public final void setName(String name)，普通，设置线程名字

3、 public final String getName()，普通，取得线程名字

但是如果要想取得线程的对象，在Thread类中有一个方法：

- 取得当前线程对象：public static Thread currentThread()；

**范例** 观察线程名称的取得：

	package cn.mldn.demo;
	
	class MyThread implements Runnable{
		@Override
		public void run() {
			for (int i = 0; i < 10; i++) {
				System.out.println(Thread.currentThread().getName() +
						", i = " + i);
			}
		}
	}
	
	public class TestDemo {
		public static void main(String[] args)  {
			MyThread mt = new MyThread();
			new Thread(mt).start();//没有设置名字
			new Thread(mt).start();//没有设置名字
			new Thread(mt,"有名线程").start();//设置名字
		}
	}
如果没有定义线程名字，则会自动分配一个线程名字，但是需要注意的是，线程名字如果设置请避免重复，同时中间不要修改名字。

**范例** 观察线程的执行结果

	package cn.mldn.demo;
	
	class MyThread implements Runnable{
		@Override
		public void run() {
				System.out.println(Thread.currentThread().getName());
		}
	}
	
	public class TestDemo {
		public static void main(String[] args)  {
			MyThread mt = new MyThread();
			mt.run();//直接通过对象调用run（）方法
			new Thread(mt).start();//通过线程调用
		}
	}

实际上可以发现主方法就是一个线程，所有的线程都是通过主线程创建并启动的。

疑问: 进程在哪里？

实际上每当使用java命令去解释程序的时候，都表示启动了一个新的JVM进程。而主方法只是这个进程上的一个线程而已。


## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course32)
