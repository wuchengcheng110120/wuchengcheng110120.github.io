## [上一页](course38)
## 【第06个代码模型】综合案例：生产者与消费者（解决重复操作问题）

现在代码中仍然存在有数据的重复设置或重复取出的问题，所以如果想要解决它就必须增加等待与唤醒机制；

参考Object类中提供的方法

1、 public final void wait() throws InterruptedException，普通方法，等待（死等）

2、 public final void notify()，普通方法，唤醒第一个等待线程

3、 public final void notifyAll()，普通方法，唤醒全部等待线程，哪个优先级高，谁有可能先执行

**范例** 通过等待与唤醒机制来解决数据的重复操作问题

	package cn.mldn.demo;
	public class TestDemo {
		public static void main(String[] args)  {
			Data data = new Data();
			new Thread(new DataProvider(data)).start();
			new Thread(new DataConsumer(data)).start();
		}
	}
	class DataProvider implements Runnable{
		private Data data;
		public DataProvider(Data data) {
			this.data = data;
		}
		@Override
		public void run() {
			for (int i = 0; i < 50; i++) {
				if (i % 2 == 0) {
					this.data.set("老李","是个好人");
				}else {
					this.data.set("民族败类","老方B");
				}
			}
		}
	}
	
	class DataConsumer implements Runnable{
		private Data data;
		public DataConsumer(Data data ) {
			this.data = data;
		}
		@Override
		public void run() {
			for (int i = 0; i < 50; i++) {
				this.data.get();
			}
		}
	}
	class Data{//负责数据保存
		private String title;
		private String note;
		// flag = true: 表示允许生产，但是不允许消费者取走
		// flag = false: 表示生产完毕，允许消费者取走，但是不允许生产
		private boolean flag = false;
		public synchronized void get() {
			if (flag == false) {//已经生产了，所以不允许重复生产
				try {
					super.wait();
				} catch (InterruptedException e) {
					e.printStackTrace();
				}// 等待执行
			}
			try {
				Thread.sleep(50);
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
			System.out.println(this.title + " = " + this.note);
			this.flag = false;
			super.notify();//唤醒等待线程
		}
		public synchronized void set(String title, String note) {
			if (flag == true) {// 现在不允许取走
				try {
					super.wait();
				} catch (InterruptedException e) {
					e.printStackTrace();
				}
			}
			this.title = title;
			try {
				Thread.sleep(100);
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
			this.note = note;	
			this.flag = true;//继续生产
			super.notify();
		}
	}

请解释sleep（）与wait（）的区别？

- sleep（）是Thread类中定义的方法，到了一定的时间后该休眠的线程可以自动唤醒；

- wait（）是Object类中定义的方法，如果要想唤醒，必须使用notify（）、notifyall（）方法才可以唤醒；




## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course40)
