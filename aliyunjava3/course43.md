## [上一页](course42)
## Runtime类

Runtime是一个运行时的描述类，在每一个JVM进程之中都会存在有一个Runtime类的对象；

这个类在查询文档的时候是无法看见构造方法的，因为其定义时将构造方法私有化了。

因为其只能有一个实例化对象，所以该类使用的是单例设计模式，那么既然是单例设计模式就一定会在类的内部提供有一个取得对象的方法：

- 取得Runtime类的对象:public static Runtime getRuntime()

那么取得了Runtime类之后，最主要的功能是可以通过它来观察当前的内存操作情况；

1、 public long freeMemory() 普通方法 取得当前空余内存空间；

2、 public long totalMemory() 普通方法 取得当前可以使用的总空间；

3、 public long maxMemory() 普通方法 取得最大的可用内存空间；

**范例** 观察内存信息取得：

	package cn.mldn.demo;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			Runtime run = Runtime.getRuntime();
			System.out.println("1、MAX = " + byteToM(run.maxMemory()));
			System.out.println("2、TOTAL = " + byteToM(run.totalMemory()));
			System.out.println("3、FREE = " + byteToM(run.freeMemory()));
			run.gc();//执行垃圾收集处理
			System.out.println("1、MAX = " + byteToM(run.maxMemory()));
			System.out.println("2、TOTAL = " + byteToM(run.totalMemory()));
			System.out.println("3、FREE = " + byteToM(run.freeMemory()));
		}
		public static double byteToM(long num) {
			return (double)num/1024/1024;
		}
	}

什么是gc()?如何处理？

- gc（Garbage Collector）：垃圾收集器

- gc 有两种处理形式，一种是自动不定期调用，另一种是使用Runtime类中的gc()方法，手工调用。


## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course44)
