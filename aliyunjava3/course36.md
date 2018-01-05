## [上一页](course35)
## 线程的同步与死锁（死锁）


同步的本质在于：一个线程等待另外一个线程执行完毕后才可以继续执行，但是如果现在相关的几个线程彼此之间都在等待着（同步了），那么就会造成死锁。

**范例** 模拟一个死锁的程序（本程序没有意义，只是为了说明问题）

	package cn.mldn.demo;
	
	class Pen {
		public synchronized void get(Note note) {
			System.out.println("我为了得到本！");
			note.result();
		}
		public synchronized void result() {
			System.out.println("为了涂鸦！");
		}
	}
	
	class Note{
		public synchronized void get(Pen pen) {
			System.out.println("我为了拿笔！");
			pen.result();
		}
		public synchronized void result() {
			System.out.println("为了上厕所！");
		}
	}
	
	public class DeadLock implements Runnable {
		private static Note note = new Note();
		private static Pen pen = new Pen();
		public static void main(String[] args) {
			new DeadLock();
		}
		public DeadLock() {
			new Thread(this).start();
			pen.get(note);
		}
		@Override
		public void run() {
			note.get(pen);
		}
	}
**console：**
	
	我为了得到本！
	我为了拿笔！

死锁一旦出现之后实际上整个程序就将暂时性中断执行了，所以死锁属于严重性问题，而这类问题出现几率不高。在整体的概念中记住：数据要想使用完整操作必须使用同步，但是过多的同步可能造成死锁。



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course37)
