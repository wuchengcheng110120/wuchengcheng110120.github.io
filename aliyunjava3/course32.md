## [上一页](course31)
## 多线程常用操作方法（线程休眠）

所谓的线程休眠指的是让线程暂缓执行一下，等到了预计的时间之后再恢复执行。

- 方法 ：public static void sleep(long millis)throws InterruptedException

	|- 休眠的时间用毫秒作为单位。

**范例** 处理休眠操作

	package cn.mldn.demo;
	
	class MyThread implements Runnable{
		@Override
		public void run() {
			for(int x = 0; x < 20; x++) {
				try {
					Thread.sleep(1000);
				} catch (InterruptedException e) {
					e.printStackTrace();
				}
				System.out.println(Thread.currentThread().getName()
						+ ", x = " + x);
			}
		}
	}
	
	public class TestDemo {
		public static void main(String[] args)  {
			MyThread mt = new MyThread();
			new Thread(mt).start();//通过线程调用
			new Thread(mt).start();//通过线程调用
			new Thread(mt).start();//通过线程调用
		}
	}

现在通过代码观察会错误的认为这三个线程是同时休眠的，但是千万要记住，所有的代码是依次进入到run（）方法中的。

![](http://ww1.sinaimg.cn/large/0060lm7Tly1fn4m5sdwesj30v70he77x.jpg)

真正进入方法的对象可能是多个也可能是一个，所以所有的进入代码的顺序可能有差异，延迟可能有差异，但是总体的执行是并发执行。



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course33)
