## [上一页](course101)

## 链表（根据索引取得数据）

public Object get（int index）{}

对于链表中的所有数据严格来讲都是有顺序的，增加顺序就是其保存顺序，所以链表本身又属于动态数组，数组就应该具备有索引取得内容的形式。

1、 在Node类中追加有一个新的方法，用于索引查找：

		//第1次调用：this = Link.root
		//第2次调用：this = Link.root.next
		public Object getNode(int index) {
			if (Link.this.foot ++ == index) {
				return this.data;
			}else {
				this.next.getNode(index);
			}
			return null;
		}

2、 在Link类里面追加有一个方法，这个方法在执行的时候必须保证链表有数据。

	public Object get(int index) {
		if (index >= this.count) {//超过了保存的个数
			return "null";
		}
		this.foot =0 ;
		return this.root.getNode(index);
	}


**范例** 根据索引实现查找：
	
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
				return "null";
			}
			this.foot =0 ;
			return this.root.getNode(index);
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
			System.out.println("======================");
			System.out.println(all.get(0));
			System.out.println(all.get(1));
			System.out.println(all.get(2));
			System.out.println(all.get(3));
		}
	}

**console：**

	hello 
	world 
	mldn 
	======================
	hello 
	world 
	mldn 
	null



## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course103)
