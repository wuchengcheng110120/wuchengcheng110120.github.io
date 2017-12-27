## [上一页](course98)

## 链表（取得链表数据个数）

在一个链表之中可以保存多个元素的数据，那么为了操作的方便就需要知道其一共需要保存的数据个数，所以需要有一个计数的统计操作。

1、 在Link类之中追加一个有统计个数的属性；

	private int count  = 0;//当前的保存个数

2、随后在每次进行数据追加的时候都应该进行一个个数的累加

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

3、 可以直接取得元素的个数

	public int size() {//取得元素个数
		return this.count;
	}

判断是否为空链表：

	public boolean isEmpty（）{}

如果根元素为null或者保存的元素个数为0，则认为链表是一个空的链表，则isEmpty（）返回的就应该是true ：

	public boolean isEmpty() {
		return this.root == null && this.count == 0;
	}

为空判断和个数可以结合在一起，不需要过多的复杂的操作逻辑。


## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course100)
