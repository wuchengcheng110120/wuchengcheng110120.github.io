## [上一页](course28)
## Java多线程实现（线程状态）


线程的启动使用的是start（）方法，但是并不意味着调用了start（）方法就立刻启动多线程。

![](http://ww3.sinaimg.cn/large/0060lm7Tly1fn3j4y7nx2j30ub0gsjvh.jpg)

当多线程调用start（）方法之后不是立刻执行，而是进入到就绪状态，等待进行调度后执行，需要将资源分配给你运行后才可以执行多线程中的代码（run（）中的），当执行了一段时间之后，你需要让出资源让其他线程来继续执行，也就是说这个时候的run（）方法可能还没执行完毕，只执行了一半，又要让出资源，随后重新进入到就绪状态，重新等待分配新资源，再继续执行。当线程执行完毕后才会进入到终止状态。





## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course30)