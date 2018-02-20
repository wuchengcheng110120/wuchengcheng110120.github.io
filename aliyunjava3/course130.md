## [上一页](course129)
##  【第18个代码模型】 List集合接口（List接口简介）

在实际的开发过程中，List集合接口的使用比率可以达到Connection系列的80%，在进行集合处理的时候优先考虑List的集合接口。首先观察List的接口中提供的方法。在这个接口里面有两个重要的扩充方法：

- 根据索引取得保存数据：public E get(int index)

- 修改数据：public E set(int index, E element)

List子接口与Connection接口相比最大的特点在于其有一个get()方法，可以根据索引取得内容。但是List本身还属于一个接口，而如果想取得接口的实例化对象，就必须有子类，在List接口下有三个常用子类：

ArrayList、Vector、LinkedList。

![](http://ww4.sinaimg.cn/large/0060lm7Tly1fomoytq42hj30vh0hjqae.jpg)

最终的操作还是应该以接口为主，那么既然主要以接口为主，所以所有的方法只要参考接口中的定义即可。



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course131)












