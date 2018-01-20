## [上一页](course59)
## 定时器

推动计算机硬件的发展核心的关键技术:时钟。所以在企业的开发之中定时也往往成为开发的重点。

JDK本身也支持这种定时调度的操作（这种操作不会被直接使用）。

如果要想实现定时调度操作处理，那么需要两个类：

- 定时调度任务定义：java.util.TimerTask；

	public abstract class TimerTask
	extends Object
	implements Runnable

		class MyTask extends TimerTask{
			@Override
			public void run() {
				System.out.println("当前时间：" +
						new SimpleDateFormat("yyyy-MM-dd HH-mm-ss.SSS").format(new Date()));
			}
		}


- 定时调度操作：java.util.Timer；

		public void schedule(TimerTask task,
		                     long delay,
		                     long period)

**范例** 定时调度:

		package cn.mldn.demo;
		
		import java.text.SimpleDateFormat;
		import java.util.Date;
		import java.util.Timer;
		import java.util.TimerTask;
		
		
		class MyTask extends TimerTask{
			@Override
			public void run() {
				System.out.println("当前时间：" +
						new SimpleDateFormat("yyyy-MM-dd HH-mm-ss.SSS").format(new Date()));
			}
		}
		
		public class TestDemo {
			public static void main(String[] args) throws Exception {
				Timer timer  = new Timer();
				//单位是毫秒ms，延迟一秒后执行，之后没两秒执行一次
				timer.schedule(new MyTask(), 1000, 2000);
			}
		}

这种操作是最原始简化的定时调度实现，以后如果在实际开发之中需要接触到更多企业级的定时调度组件。

定时调度和多线程有关联。


## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course61)
