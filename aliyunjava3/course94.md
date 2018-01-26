## [上一页](course93)
##  【第13个代码模型】对象序列化（transient关键字）

实际上序列化的处理在java.io包中有两类，Serializable是使用最多的序列化接口，这种操作采用自动化的模式完成，也就是说默认情况下所有的属性都会被序列化。

还有一个接口Interface Externalizable是需要用户自己动手序列化处理。

但是由于默认情况Serializable接口会将类中所有的属性进行保存，但是如果现在某些类中的属性不希望被保存了，可以使用transient关键字。

**范例** 使用transient：

	private  transient String name;
	private int age;

不过在大部分情况下，序列化是在简单Java类中使用，在其他类上使用序列化的情况较少，如果是简单java类就很少去使用transient关键字了。



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course95)
