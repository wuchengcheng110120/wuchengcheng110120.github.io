## [上一页](course95)

## 链表（链表基本概念）

简单的数据结构面试题必须掌握，数组排序、链表、二叉树等；所以对于数据结构的掌握也已经成为了面试的基本功。

数据结构主要的核心组成：引用 + 递归；

链表的基本介绍：如果想要保存多个对象，那么首先可以想到的概念就只有对象数组，同时如果该数组可以保存任意的对象，又可以想到的一定是Object型的数组：

Object data []  =  new Object [3];

在实际的开发过程中面临的一个问题：数组是一个定长的线性结构，也就是说虽然以上的代码可以满足于存放多个内容，但是一旦我们的内容不足或者是内存过多都有可能造成内存的浪费。如果此时想要解决此类问题最好的做法就是不定义一个固定长度的数组，有多少数据就保存多少数据。可以采用火车车厢类似的设计模式，动态的进行车厢的挂载，假设每节车厢只保留一个数据，那么现在假设可以不受内存的限制，就可以证明解决了数组长度问题。

如果想要定义火车车厢，肯定不可能只保留一个数据，因为还需要另外一个指向，指向下一个节点.

虽然设置好了关系，但是里面存放的毕竟都是数据，真正需要的时候一定需要将数据一次取出那么这个时候肯定用递归的方式。

![](http://ww1.sinaimg.cn/large/0060lm7Tly1fmv7d7rv3pj30i705kdhw.jpg)

**范例** 链表的基本雏形：

	class Node {//只有Node类才可以在保存数据的同时设置数据的先后关系
		private Object data;//真正要保存的数据
		private Node next;//定义下一个节点
		public Node(Object data) { // 保存数据的载体
			this.data = data;
		}
		public void setData(Object data) {
			this.data = data;
		}
		public Object getData() {
			return this.data;
		}
		public void setNext(Node next) {
			this.next = next;
		}
		public Node getNext() {
			return this.next;
		}
	}
	
	
	public class TestLinkDemo {
	
		public static void main(String[] args) throws Exception {
			//1、封装几个节点
			Node root = new Node("火车头");//现在假设存放的数据是String
			Node n1 = new Node("车厢A");
			Node n2 = new Node("车厢B");
			Node n3 = new Node("车厢C");
			//2、需要设置节点的关系
			root.setNext(n1);
			n1.setNext(n2);
			n2.setNext(n3);
			//3、输出节点
			print(root);
		}
		public static void print(Node node) {
			if (node != null) {//表示当前有节点
				System.out.println(node.getData());
				print(node.getNext());
			}		
		}
	}

**console：**

	火车头
	车厢A
	车厢B
	车厢C

结论： 在整个链表的实现过程之中Node的核心作用在于：保存数据和连接节点关系，在以上的代码中比较麻烦，因为发现客户端需要（主方法）需要自己来进行节点的创建，以及关系的配置。所以所谓的链表就是需要有一个单独的类，假设：Link，同过这个类来实现Node类的数据保存和关系处理。

## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course97)
