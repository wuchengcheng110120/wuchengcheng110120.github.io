## [上一页](course62)
## 【第08个代码模型】ThreadLocal类

以后的项目里面ThreadLocal类可以帮我们减少一些重要的引用传递。

在讲解具体的概念之前首先来观察如下的一段程序：

	package cn.mldn.demo;
	
	class Message{
		private String note;
	
		public String getNote() {
			return note;
		}
	
		public void setNote(String note) {
			this.note = note;
		}
	}
	
	class MessageConsumer{
		public void print(Message msg) {//必须明确接收Message类对象
			System.out.println(Thread.currentThread().getName() + "= " +msg.getNote());
		}
	}
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			new Thread(()->{
				Message msg = new Message();
				msg.setNote("www.mldn.cn");
				new MessageConsumer().print(msg);
			},"用户A").start();
			new Thread(()->{
				Message msg = new Message();
				msg.setNote("明天可以睡懒觉了！");
				new MessageConsumer().print(msg);
			},"用户B").start();
		}
	}

**console：**

	用户A= www.mldn.cn
	用户B= 明天可以睡懒觉了！

以上的代码之中明确的使用了引用传递，将Message类的对象传递给了MessageConsumer类的print()方法。

	package cn.mldn.demo;
	
	class Message{
		private String note;
	
		public String getNote() {
			return note;
		}
	
		public void setNote(String note) {
			this.note = note;
		}
	}
	
	class MessageConsumer{
		public void print() {//必须明确接收Message类对象
			System.out.println(Thread.currentThread().getName() + "= " +MyUtil.message.getNote());
		}
	}
	
	class MyUtil{
		public static Message message;
	}
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			new Thread(()->{
				Message msg = new Message();
				msg.setNote("www.mldn.cn");
				MyUtil.message = msg;
				new MessageConsumer().print();
			},"用户A").start();
			new Thread(()->{
				Message msg = new Message();
				msg.setNote("明天可以睡懒觉了！");
				MyUtil.message = msg;
				new MessageConsumer().print();
			},"用户B").start();
		}
	}

**console：**

	用户B= www.mldn.cn
	用户A= www.mldn.cn

![](http://ww2.sinaimg.cn/large/0060lm7Tly1fno44xv7mij30vg0hmteg.jpg)

所以现在想要标记出每一个线程的具体对象信息，就需要使用ThreadLocal，这里面在进行数据保存的时候多保存了一个currentThread。本类定义如下：

public class ThreadLocal<T>
extends Object

在这个类中有以下重要方法：

- 取得数据：public T get()

- 保存数据：public void set(T value)

- 删除数据：public void remove()

**范例** 利用ThreadLocal来解决当前问题：

	package cn.mldn.demo;
	
	import java.util.Set;
	
	class Message{
		private String note;
	
		public String getNote() {
			return note;
		}
	
		public void setNote(String note) {
			this.note = note;
		}
	}
	
	class MessageConsumer{
		public void print() {//必须明确接收Message类对象
			System.out.println(Thread.currentThread().getName() + "= " +MyUtil.get().getNote());
		}
	}
	
	class MyUtil{
		private static ThreadLocal<Message> threadLocal = new ThreadLocal<Message>();
		public static void set(Message msg) {
			threadLocal.set(msg);
		}
		public static Message get() {
			return threadLocal.get();
		}
	}
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			new Thread(()->{
				Message msg = new Message();
				msg.setNote("www.mldn.cn");
				MyUtil.set(msg);
				new MessageConsumer().print();
			},"用户A").start();
			new Thread(()->{
				Message msg = new Message();
				msg.setNote("明天可以睡懒觉了！");
				MyUtil.set(msg);
				new MessageConsumer().print();
			},"用户B").start();
		}
	}
**console：**

	用户B= 明天可以睡懒觉了！
	用户A= www.mldn.cn

一个项目中最重要的对象就是资源连接信息，例如：数据库；

以后项目开发，ThreadLocal会作为初期项目实现的基础。



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course64)
