## [上一页](course36)
## 【第06个代码模型】综合案例：生产者与消费者（基础模型）

生产者和消费者是一个最为经典的供求案例，而像这种供求案例：provider、consumer。在以后进行各种分布式的结构开发之中，都会被大量的采用。

现在假设目的： 希望生产者负责生产数据，而生产者每生成一个完整的数据之后，消费者就要把这些数据取走。于是，假设要生成如下的数据：

- title = 老李， note = 是一个好人；

- title = 民族败类， note = 老方B；

![](http://ww1.sinaimg.cn/large/0060lm7Tly1fn5kmyffgrj30v90headw.jpg)

**范例** 编写程序的基础模型：

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
					this.data.setTitle("老李");
					try {
						Thread.sleep(1000);
					} catch (InterruptedException e) {
						e.printStackTrace();
					}
					this.data.setNote("是个好人");
				}else {
					this.data.setTitle("民族败类");
					try {
						Thread.sleep(1000);
					} catch (InterruptedException e) {
						e.printStackTrace();
					}
					this.data.setNote("老方B");
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
				try {
					Thread.sleep(800);
				} catch (InterruptedException e) {
					e.printStackTrace();
				}
				System.out.println(this.data.getTitle() + " = " + this.data.getNote());
			}
		}
	}
	
	class Data{//负责数据保存
		private String title;
		private String note;
		public void setTitle(String title) {
			this.title = title;
		}
		public void setNote(String note) {
			this.note = note;
		}
		public String getNote() {
			return note;
		}
		public String getTitle() {
			return title;
		}
	}

这个时候已经可以发现程序中会存在有两类问题：

- 数据不完整，好人 = 败类；

- 数据的重复操作问题（重复设置或重复取出）。



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course38)
