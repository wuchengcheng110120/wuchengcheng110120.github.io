## [上一页](course99)

## 链表（链表数据转换为对象数组）

public Object[] toArray（）{}

首先链表是一个动态对象数组，那么既然是动态对象数组，返回的内容也一定就应该是一个对象数组。但是如果要想进行一个数组的返回，首先必须要开辟一个数组（数组长度就是count属性的内容），同时这个的数组内容的填充应该依次将节点中的内容取出才可以正常完成。

![](http://ww3.sinaimg.cn/large/0060lm7Tly1fmvfxfds6kj30v80hetft.jpg)

1、 在Link类中一定会存在有toArray（）的方法，该方法的返回值一定是Object[]；

2、所有在返回的对象数组中的数据都在Node类里面，那么就证明这些数据应该在Node类中利用递归来依次取出；那么应该在外部类Link中定义一个返回类型的属性；

	private Object[] retData;//返回类型
	private int foot = 0;//操作角标

3、 在Node中处理节点数据：
	
	//第1次调用：this = Link.root
		//第2次调用：this = Link.root.next
		public void toArrayNode() {
			Link.this.retData[Link.this.foot++] = this.data;
			if (this.next != null) {//现在还有下一个节点
				this.next.toArrayNode();
			}
		}

数据的存储和返回是在开发之中链表使用最多的功能。
	

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
			//第1次调用：this = Link.root
			//第2次调用：this = Link.root.next
			public void toArrayNode() {
				Link.this.retData[Link.this.foot++] = this.data;
				if (this.next != null) {//现在还有下一个节点
					this.next.toArrayNode();
				}
			}
		}
		//-----------------------Link类-----------
		private Object[] retData;//返回类型
		private int foot = 0;//操作角标
		private int count  = 0;//当前的保存个数
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
			this.count++;
		}	
		public int size() {//取得元素个数
			return this.count;
		}
		public boolean isEmpty() {
			return this.root == null && this.count == 0;
		}
		public Object[] toArray() {
			if (this.count == 0) {
				return null;
			}
			//现在链表中存在有数据，则开辟指定长度的数组
			//该数组一定要交给Node类进行处理。
			this.retData = new Object[this.count];
			this.foot = 0;//进行清零的处理，需要进行角标的操作
			this.root.toArrayNode();//将数据的取出操作交给Node类完成
			return retData;
		}
	}
	public class TestLinkDemo {
	
		public static void main(String[] args) throws Exception {
			Link all = new Link();
			all.add("hello ");
			all.add("world ");
			all.add("mldn ");
			Object result[] = all.toArray();
			for (int i = 0; i < result.length; i++) {
				System.out.println(result[i]);
			}
		}
	}

**console：**

	hello 
	world 
	mldn 



## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course101)
