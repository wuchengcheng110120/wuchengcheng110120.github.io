## [上一页](course114)
##  volatile关键字

单例设计模式的本质在于构造方法被私有化，而后通过类内部的static方法取得实例化对象，而单例设计有两种形式：懒汉式（使用时进行实例化）和饿汉式（在类加载时进行实例化）。

**范例** 观察懒汉式程序设计的问题：

	package cn.mldn.demo;
	
	class Sington{
		private static Sington instance; // 懒汉式所以不会进行对象实例化
		private Sington() {
			System.out.println("【构造方法】" + Thread.currentThread().getName());
		}
		public static Sington getInstance() {
			if (instance == null) {
				instance = new Sington();
			}
			return instance;
		}
	}
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			new Thread(()->Sington.getInstance(), "线程A").start();
			new Thread(()->Sington.getInstance(), "线程B").start();
			new Thread(()->Sington.getInstance(), "线程C").start();
			new Thread(()->Sington.getInstance(), "线程D").start();
			new Thread(()->Sington.getInstance(), "线程E").start();
		} 	
	}

**console：**

	【构造方法】线程B
	【构造方法】线程A

这个时候发现，单例设计不再是单例了，而变成了多个重复的实例化对象的类。造成这种问题的关键就在于线程的不同步问题，也就是说在第一次实例化instance对象的时候，有可能有多个线程同时进入了getInstance()方法，那么就有可能实例化多次对象。

![](http://ww4.sinaimg.cn/large/0060lm7Tly1fo9bd88pycj30v70hgjx0.jpg)

那么这个时候可能想到的第一个解决方案就是：使用synchronized同步。代码修改如下：

	package cn.mldn.demo;
	
	class Sington{
		private static Sington instance; // 懒汉式所以不会进行对象实例化
		private Sington() {
			System.out.println("【构造方法】" + Thread.currentThread().getName());
		}
		public static synchronized Sington  getInstance() {
			if (instance == null) {
				instance = new Sington();
			}
			return instance;
		}
	}
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			new Thread(()->Sington.getInstance(), "线程A").start();
			new Thread(()->Sington.getInstance(), "线程B").start();
			new Thread(()->Sington.getInstance(), "线程C").start();
			new Thread(()->Sington.getInstance(), "线程D").start();
			new Thread(()->Sington.getInstance(), "线程E").start();
		} 	
	}

现在看起来问题的确解决了，因为同步有了锁，不会多个线程同时进入。但是这个代码出现了性能瓶颈，如果在高并发的访问状态下，那么本操作就将导致系统性能下降。那么这个时候就必须依靠volatile关键字来解决此类问题了（不仅仅是一个同步的问题）。

![](http://ww1.sinaimg.cn/large/0060lm7Tly1fo9bl1oc55j30v60hetf0.jpg)

volatile关键字的使用区别：

- 如果现在没有使用volatile关键字定义的变量，则操作的时候使用的是副本进行处理，那么副本进行原始数据之间的同步就要产生延迟，而所谓的线程的不同步原因也在于此；

- volatile关键字定义的变量将直接使用原始数据进行处理，更改后立即生效。

**范例** 使用volatile关键字解决问题：

	package cn.mldn.demo;
	
	class Sington{
		private static volatile Sington instance; // 懒汉式所以不会进行对象实例化
		private Sington() {
			System.out.println("【构造方法】" + Thread.currentThread().getName());
		}
		public static  Sington  getInstance() {// 如果要想保证性能高，此方法就不能使用同步
			if (instance == null) {
				synchronized (Sington.class) {
					if (instance == null) {
						instance = new Sington();
					}
				}
			}
			return instance;
		}
	}
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			new Thread(()->Sington.getInstance(), "线程A").start();
			new Thread(()->Sington.getInstance(), "线程B").start();
			new Thread(()->Sington.getInstance(), "线程C").start();
			new Thread(()->Sington.getInstance(), "线程D").start();
			new Thread(()->Sington.getInstance(), "线程E").start();
		} 	
	}

以后编写的代码会很少涉及到此关键字的使用，但是在面试之中会经常被问到
	

## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course116)
