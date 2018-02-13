## [上一页](course128)
##  Collection集合接口

在Java的类集里面（java.util包）提供有两个最为核心的操作接口: Collection接口、Map接口，	其中Collection接口的一个操作形式与之前编写链表的操作形式类似。每一次进行数据操作的时候只能够对单个对象进行处理。

所以Collection是单个集合保存的最大父接口。Collection的接口定义如下：


public interface Collection<E>
extends Iterable<E>

从JDK1.5开始发现Collection接口上追加有泛型应用，这样的好处就是可以避免了ClassCastException，里面所有数据的保存类型应该是相同的。在JDK1.5之前Iterable接口中的iterator()是直接在Connection接口里定义的。对于此接口的常用方法有以下几个：

普通方法：public boolean add(E e)，向集合中添加数据；

普通方法：public boolean addAll(Collection<? extends E> c)，向集合中添加一组数据；

普通方法：public void clear()，清空集合数据；

普通方法：public boolean contains(Object o)， 查找数据是否存在，需要使用equals方法；

普通方法：public boolean isEmpty()，判断是否为空；

普通方法：public boolean remove(Object o)，删除数据，需要equals方法；

普通方法：public int size()，取得集合长度；

普通方法：public Object[] toArray()，将集合变为对象数组返回；

普通方法：public Iterator<E> iterator()，取得Iterator接口对象，用于输出；

在开发之中按照使用的比例来说add()和iterator()占用了使用频率的95%以上，其他方法使用较少。但是需要说明的一点是在实际的开发之中，我们很少会去直接使用Connection接口（十几年前使用最多的可能是Connection接口）。因为Connection接口只是一个存储数据的标准，而并不能区分存储的类型，例如：如果要存放数据可能需要区分重复与不重复。所以在实际的开发之中，往往会去考虑使用Connection接口的两个子接口：List（允许重复）、Set（不允许重复）。

![](https://s1.ax1x.com/2018/02/13/9YSdEj.png)

Collection接口中有两个重要的方法add()和iterator()。子接口同时有这两个方法。


## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course130)
