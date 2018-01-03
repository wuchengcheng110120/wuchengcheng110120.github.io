## [上一页](course29)
## Java多线程实现（Callable实现多线程）



从JDK1.5之后追加了一个新的开发包：java.util.concurrent，这个开发包主要是进行高性能编程使用的，也就是说在这个开发包里面高并发操作中才会使用到的类。在这个包里面定义有一个新的接口：

	@FunctionalInterface
	public interface Callable<V>{
		public V call() throws Exception;
	}

Runnable中的run（）方法虽然也是线程的主方法，但是其没有返回值，因为它的方法遵循了主方法的设计原则，线程开始了就别回头。但是很多时候需要一些返回值，例如当某些线程执行完成后有可能带来一些返回结果，这种情况下就只能够利用Callable来实现多线程。

**范例** 使用Callable定义线程主体类：

	class MyThread implements java.util.concurrent.Callable<String>{
		@Override
		public String call() throws Exception {
			for (int i = 0; i < 20; i++) {
				System.out.println("卖票， i = " + i);
			}
			return "票卖完了,下次吧。。。";
		}
	}

不管何种情况，如果要启动多线程只有Thread类的start（）方法。于是来分析一下Callable接口的定义：
	
	public interface Callable<V>{
		public V call()throws Exception
	}

	public FutureTask(Callable<V> callable)

	public class FutureTask<V>
	extends Object
	implements Runnable，Future<V>

	public interface RunnableFuture<V>
	extends Runnable, Future<V>

	public interface Future<V>{
		public V get()throws InterruptedException,ExecutionException
	}

	@FunctionalInterface
	public interface Runnable

	public class Thread
	extends Object
	implements Runnable{
		public void start()	
	}

![](http://ww1.sinaimg.cn/large/0060lm7Tly1fn3k5sabwuj30u60gu7aq.jpg)

**范例** 启动并取得多线程的结果：

	package cn.mldn.demo;
	
	import java.util.concurrent.ExecutionException;
	import java.util.concurrent.FutureTask;
	
	class MyThread implements java.util.concurrent.Callable<String>{
		@Override
		public String call() throws Exception {
			for (int i = 0; i < 10; i++) {
				System.out.println("卖票， i = " + i);
			}
			return "票卖完了,下次吧。。。";
		}
	}
	
	public class TestDemo {
		public static void main(String[] args) throws InterruptedException, ExecutionException {
			FutureTask<String> task = new FutureTask<String>(new MyThread());
			new Thread(task).start(); //启动多线程
			System.out.println(task.get());
		}
	}

这种形式主要是返回处理结果。



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course31)
