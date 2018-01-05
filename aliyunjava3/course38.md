## [上一页](course37)
## 【第06个代码模型】综合案例：生产者与消费者（解决同步问题）

如果想要解决同步问题，首先可以想到synchronized关键字来定义同步的操作方法。

代码修改如下：

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
		public synchronized void get() {
			try {
				Thread.sleep(50);
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
			System.out.println(this.title + " = " + this.note);
		}
		public synchronized void set(String note, String title) {
			this.title = title;
			try {
				Thread.sleep(100);
			} catch (InterruptedException e) {
				e.printStackTrace();
			}
			this.note = note;	
		}
	}

现在发现程序中数据的同步问题得到了解决，但是重复操作问题依然存在。



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course39)
