## [上一页](course96)

## 链表（链表实现结构说明）


如果按照以上的方式进行链表的实现对于开发者而言会非常的痛苦，因为所有的使用者必须自己来处理数据的关系，所以为了更好的处理应该追加有一个程序类来完成，假设这个类就称为Link类。

![](http://ww3.sinaimg.cn/large/0060lm7Tly1fmvbtvhqppj30vc0hathc.jpg)

但是如果对于程序的初期结构采用如下的方式定义，也会出现如下问题:

	class Link {//负责链表的操作
		private class Node {//负责数据与节点关系的匹配
		}
	}

使用内部类可以保证只有Link类才有权操作Node类，而且使用了内部类之后还有一个最明显的特点：内部类和外部类可以方便的进行私有属性的访问，也就是避免了setter与getter方法的尴尬。

**范例** 基础的定义结构：

	class Link {//负责链表的操作
		private class Node {//负责数据与节点关系的匹配
			private Object data;// 保存节点数据
			private Node next;//保存下一个节点
			public Node(Object data) {
				this.data  = data;
			}
		}
		//-----------------------Link类
		
	}

而后按照以上的模式就可以编写代码，但是对于链表的核心功能：增加、修改、删除、取出数据、判断某一数据是否存在。





## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course98)
