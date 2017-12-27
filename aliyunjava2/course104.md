## [上一页](course103)

## 链表（删除数据）


public void remove（Object data）{}

如果需要进行数据的删除处理，则需要考虑两种情况：

情况一： 要删除的是根节点

如果要删除的是根节点，则意味着Link中的根节点的保存需要发生变化，该操作主要在Link类中处理；

情况二： 要删除的不是根节点

所有的操作应该交给Node处理；

![](http://ww2.sinaimg.cn/large/0060lm7Tly1fmviskmwxmj30vc0hatih.jpg)

1、 修改Node的程序类：

	//第1次调用：this = Link.root.next;
		//第2次调用：this = Link.root.next.next、previous = Link.root.next;
		public void removeNode(Node previous, Object data) {
			if (this.data.equals(data)) {//当前节点为要删除节点
				previous.next = this.next;//删除当前了
			}else {
				this.next.removeNode(this, data);
			}
		}

2、修改Link的程序类

	public void remove(Object data) {
		if (this.contains(data)) {//如果该数据存在则进行删除处理
			if (this.root.data.equals(data)) {//首先要判断要删除的节点是否为根节点
				this.root = this.root.next;//根节点变为下一个节点
			}else {//不是根节点
				this.root.removeNode(this.root,data);
			}
			this.count--;
		}
	}

**范例** 删除数据：

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
			//第1次调用：this = Link.root
			//第2次调用：this = Link.root.next
			public boolean containsNode(Object search) {
				if (search .equals(this.data)) {//找到了
					return true;
				}else {
					if (this.next != null) {//当前节点之后还有其他节点
						return this.next.containsNode(search);
					}else {
						return false;
					}
				}
			}
			//第1次调用：this = Link.root
			//第2次调用：this = Link.root.next
			public Object getNode(int index) {
				if (Link.this.foot ++ == index) {
					return this.data;
				}else {
					return this.next.getNode(index);
				}
			}
			//第1次调用：this = Link.root
			//第2次调用：this = Link.root.next
			public void setNode(int index, Object newData) {
				if (Link.this.foot++ == index) {//索引相同
					this.data = newData;
				}else {
					if (this.next != null) {
						this.next.setNode(index, newData);
					} 
				}
			}
			//第1次调用：this = Link.root.next;
			//第2次调用：this = Link.root.next.next、previous = Link.root.next;
			public void removeNode(Node previous, Object data) {
				if (this.data.equals(data)) {//当前节点为要删除节点
					previous.next = this.next;//删除当前了
				}else {
					this.next.removeNode(this, data);
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
		public boolean contains(Object search) {
			//没有要查询的内容，以及链表为空
			if (search == null || this.root == null) {
				return false;
			}
			return this.root.containsNode(search);
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
		public Object get(int index) {
			if (index >= this.count) {//超过了保存的个数
				return null;
			}
			this.foot =0 ;
			return this.root.getNode(index);
		}
		public void set(int index, Object newData) {
			if (index >= this.count) {//超过了保存的个数
				return;//结束方法调用
			}
			this.foot = 0;
			this.root.setNode(index, newData);
		}
		public void remove(Object data) {
			if (this.contains(data)) {//如果该数据存在则进行删除处理
				if (this.root.data.equals(data)) {//首先要判断要删除的节点是否为根节点
					this.root = this.root.next;//根节点变为下一个节点
				}else {//不是根节点
					this.root.removeNode(this.root,data);
				}
				this.count--;
			}
		}
	}
	public class TestLinkDemo {
		public static void main(String[] args) throws Exception {
			Link all = new Link();
			all.add("hello ");
			all.add("world ");
			all.add("mldn ");
			all.set(0, "你好");
			all.remove("你好");
			all.remove("mldn ");
			Object result[] = all.toArray();
			for (int i = 0; i < result.length; i++) {
				System.out.println(result[i]);
			}
			System.out.println("======================");
			System.out.println(all.get(0));
			System.out.println(all.get(1));
			System.out.println(all.get(2));
			System.out.println(all.get(3));
		}
	}

**console：**

	world 
	======================
	world 
	null
	null
	null

这就是最简化的链表。

整个的设计只是完成了一个简单的单向链表，也没有考虑到过多的性能，但是至少要通过此链表弄清楚动态数组的实现原理。一定要清楚contains（）与remove（）两个方法需要equals（）支持


## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course105)
