## [上一页](course40)
## 线程池（线程池实现）

1、 创建无限大小的线程池：

	package cn.mldn.demo;
	
	import java.util.concurrent.ExecutorService;
	import java.util.concurrent.Executors;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			//创建了一个线程池的模型，但是里面没有线程
			ExecutorService eService = Executors.newCachedThreadPool();
			for (int i = 0; i < 10; i++) {
				//Thread.sleep(200);
				int index = i;
				eService.submit(()->{
					System.out.println(Thread.currentThread().getName() + " i = "
							+ index );
				});
			}
			eService.shutdown();
		}
	}
**console：**

	pool-1-thread-1 i = 0
	pool-1-thread-5 i = 4
	pool-1-thread-6 i = 5
	pool-1-thread-4 i = 3
	pool-1-thread-7 i = 6
	pool-1-thread-3 i = 2
	pool-1-thread-2 i = 1
	pool-1-thread-6 i = 7
	pool-1-thread-3 i = 9
	pool-1-thread-2 i = 8


2、 创建单线程的线程池：

	package cn.mldn.demo;
	
	import java.util.concurrent.ExecutorService;
	import java.util.concurrent.Executors;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			//创建了一个线程池的模型，但是里面没有线程
			ExecutorService eService = Executors.newSingleThreadExecutor();
			for (int i = 0; i < 10; i++) {
				//Thread.sleep(200);
				int index = i;
				eService.submit(()->{
					System.out.println(Thread.currentThread().getName() + " i = "
							+ index );
				});
			}
			eService.shutdown();
		}
	}

**console：**

	pool-1-thread-1 i = 0
	pool-1-thread-1 i = 1
	pool-1-thread-1 i = 2
	pool-1-thread-1 i = 3
	pool-1-thread-1 i = 4
	pool-1-thread-1 i = 5
	pool-1-thread-1 i = 6
	pool-1-thread-1 i = 7
	pool-1-thread-1 i = 8
	pool-1-thread-1 i = 9

3、 创建固定大小的线程池;

	package cn.mldn.demo;
	
	import java.util.concurrent.ExecutorService;
	import java.util.concurrent.Executors;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			//创建了一个线程池的模型，但是里面没有线程
			ExecutorService eService = Executors.newFixedThreadPool(3);
			for (int i = 0; i < 10; i++) {
				//Thread.sleep(200);
				int index = i;
				eService.submit(()->{
					System.out.println(Thread.currentThread().getName() + " i = "
							+ index );
				});
			}
			eService.shutdown();
		}
	}
**console:**

	pool-1-thread-1 i = 0
	pool-1-thread-2 i = 1
	pool-1-thread-2 i = 3
	pool-1-thread-2 i = 5
	pool-1-thread-3 i = 2
	pool-1-thread-2 i = 6
	pool-1-thread-1 i = 4
	pool-1-thread-2 i = 8
	pool-1-thread-3 i = 7
	pool-1-thread-1 i = 9

4、 定时调度线程池：

	package cn.mldn.demo;
	
	import java.util.concurrent.ExecutorService;
	import java.util.concurrent.Executors;
	import java.util.concurrent.ScheduledExecutorService;
	import java.util.concurrent.TimeUnit;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			//创建了一个具有三个线程大小的定时调度线程池
			ScheduledExecutorService eService = Executors.newScheduledThreadPool(1);
			for (int i = 0; i < 10; i++) {
				Thread.sleep(200);
				int index = i;
				eService.scheduleAtFixedRate(new Runnable() {
					@Override
					public void run() {
						System.out.println(Thread.currentThread().getName() + " i = "
								+ index );
					}
				}, 3, 2, TimeUnit.SECONDS);// 使用的是秒的单位，表示延迟3s，周期2秒
			}
		}
	}

线程池给开发者带来的好处是允许多个开发者按照组的模式进行程序的处理，这样在某一个业务逻辑非常复杂的环境下，性能就可以得到很好的提升。


## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course42)
