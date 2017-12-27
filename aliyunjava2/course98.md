## [上一页](course97)

## 链表（增加链表数据）

public void add(Object data）

如果要想在链表之中实现一个数据的增加操作，则应该在链表里面提供有一个追加方法，而这个追加方法上的参数应该是Object类型。

1、 在Link类中追加新的方法定义：

	public void add(Object data) {
			if (data == null) {//人为的追加了规定，不允许存放null
				return ;//方法结束调用
			}
		}

2、进行数据的保存，应该首先定义一个根节点，因为只有找到了根节点，才能后续添加后面的子节点：

根节点的类型一定就是Node，则应该在Link类里面追加有一个Node类的属性。

	private Node root; //属于根节点，没根节点就无法进行 数据的保存

3、后续节点操作；

![](http://ww1.sinaimg.cn/large/0060lm7Tly1fmvdjl8trgj30vf0hh46s.jpg)


**范例** 链表增加数据：

	class Link {//负责链表的操作
		private class Node {//负责数据与节点关系的匹配
			private Object data;// 保存节点数据
			private Node next;//保存下一个节点
			public Node(Object data) {
				this.data  = data;
			}
			//第1次调用：this = Link.root
			//第2次调用：this = Link.root.next
			//第3次调用：this = Link.root.next.next
			public void addNode (Node newNode) {//处理节点关系
				if (this.next == null) {//当前节点下一个为空，表示可以保存
					this.next =newNode;
				} else {//当前节点的下一个不为空
					this.next.addNode(newNode);
				}
			}
		}
		//-----------------------Link类-----------
		private Node root; //属于根节点，没根节点就无法进行 数据的保存
		public void add(Object data) {
			if (data == null) {//人为的追加了规定，不允许存放null
				return ;//方法结束调用
			}
			//如果想要进行数据的保存，那么必须将数据封装在Node节点类里面
			//如果没有封装，则无法确认好节点的先后顺序
			Node newNode = new Node(data);
			if (this.root == null) {//当前没有根节点
				this.root = newNode;//第一个节点设置为根节点
			}else {//根节点已经存在
				//应该把此时的节点顺序的处理交给Node类自己来完成
				this.root.addNode(newNode);
			}
		}	
	}
	public class TestLinkDemo {
	
		public static void main(String[] args) throws Exception {
			Link all = new Link();
			all.add("hello ");
			all.add("world ");
			all.add("mldn ");
		}
	}

这个时候理论上如果内存够大，那么可以存放的内容就非常的多了，而整个代码的实现关键就在于Node类负责数据保存和节点关系匹配。



## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course99)
