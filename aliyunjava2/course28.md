## [上一页](course27)

## 8.4 String类的常用方法（字符串比较）

之前使用过“equals（）”方法，该方法本身是可以进行区分大小写的相等判断，而除了这个方法之外String类里面还提供有如下的几个比较操作：

 No.| 方法名称 | 类型 | 描述
 -|---|------|------|
 01| public boolean equals(Object anObject)  |普通 | 区分大小写的比较
 02| public boolean equalsIgnoreCase(String anotherString) |  普通 | 不区分大小写比较 
 03| public int compareTo(String anotherString) | 普通 | 比较两个字符串的大小关系

**范例** 不区分大小写比较：

	public class StringDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub		
			String str = "hello";
			System.out.println("Hello".equals(str));
			System.out.println("Hello".equalsIgnoreCase(str));
		}
	}

**console：**

	false
	true

在String类中compareTo（）方法是一个最为重要的操作方法，该方法返回的是int型数据，该数据会根据大小关系返回有三类的内容：

- 相等：返回0；

- 小于：返回的内容小于0；

- 大于：返回的内容大于0；

**范例** compareTo（）比较：

	public class StringDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub		
			System.out.println("A".compareTo("a"));
			System.out.println("a".compareTo("A"));
			System.out.println("a".compareTo("a"));
			System.out.println("ab".compareTo("ac"));
			System.out.println("abc".compareTo("a"));
			System.out.println("范".compareTo("周"));//没有意义
		}
	}


**console：**

	32
	0
	-1
	2
	11931

compareTo（）是唯一一个可以区分大小关系的方法。以后会有更加详细的讲解。


## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course29)
