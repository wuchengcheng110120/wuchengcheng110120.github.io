## [上一页](course36)

## 10 引用传递进阶分析

引用传递是java的核心，如果不懂引用传递，所有的代码都无法正常分析。

下面使用简单的几个程序来对引用传递进行分析。

**范例**  引用传递一： 

	class Message{
		private int num;
		public void setNum(int num) {
			this.num = num;
		}
		public int getNum() {
			return this.num;
		}
	}
	
	public class TestDemo {
	
		public static void main(String[] args) {
			Message msg =  new Message();
			msg.setNum(100);
			fun(msg);
			System.out.println(msg.getNum());
		}
		
		public static void fun(Message temp) {
			temp.setNum(30);
		}
	}

**console： **

	30	

![](https://i.imgur.com/dvqeJSK.png)

**范例** 引用传递二： 

	public class TestDemo {
	
		public static void main(String[] args) {
			String str = "hello";
			fun(str);
			System.out.println(str);
		}
		
		public static void fun(String temp) {
			temp = "world" ;
		}
	}

**console：**

	hello

![](https://i.imgur.com/eHIemS8.png)

最终结果还是“hello”。本例分析的关键在于：字符串常量一旦声明则不可改变，字符串对象的内容改变依靠的是地址的引用关系变更。

**范例** 引用传递三：

	class Message{
		private String note;
		public void setNote(String note) {
			this.note = note;
		}
		public String getNote() {
			return this.note;
		}
	}
	
	public class TestDemo {
	
		public static void main(String[] args) {
			Message msg = new Message();
			msg.setNote("hello");
			fun(msg);
			System.out.println(msg.getNote());		
		}	
		public static void fun(Message temp) {
			temp.setNote("world") ;
		}
	} 

**console：**

	world




![](https://i.imgur.com/sFJz6wk.png)

String类是引用数据类型，应该按照引用数据类型进行分析：

![](https://i.imgur.com/1y3CU3w.png)

> 把String类的使用当作基本数据类型来操作；

## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course38)
