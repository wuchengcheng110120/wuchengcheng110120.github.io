## [上一页](course39)
## 线程池（线程池概念）

所谓线程池就是多个线程封装在一起进行工作。

![](https://s1.ax1x.com/2018/01/08/pm4mUP.png)

从JDK1.5之后追加了一个并发程序的访问包：java.util.concurrent，对于线程池操作的核心类和接口就定义在此包之中，这里面有两个核心的接口：

- 普通的执行线程池定义： java.util.concurrent.Interface ExecutorService

- 调度线程池： java.util.concurrent.Interface ScheduledExecutorService

那么如果要进行线程池的创建，可以使用java.util.concurrent.Executors类来完成，有如下几个方法：

- 创建无大小限制的线程池：public static ExecutorService newCachedThreadPool()

- 创建固定大小的线程池：public static ExecutorService newFixedThreadPool(int nThreads)

- 创建单线程池：public static ScheduledExecutorService newSingleThreadScheduledExecutor()

- 创建定时调度池：public static ScheduledExecutorService newScheduledThreadPool(int corePoolSize)



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course41)


