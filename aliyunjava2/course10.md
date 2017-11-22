## [上一页](course9)

## 6.2 数组引用传递

既然数组本身也属于引用数据类型，那么也一定可以发生引用传递。

在这之前首先来研究一下数组的空间开辟

**范例** 观察一个程序：

	public class ArrayDemo {
	
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			int data [] = null;
			data  = new int [3];
			data[0] = 10;//第1个元素
			data[1] = 20;//第2个元素
			data[2] = 30;//第3个元素
		}
	}

![](https://i.imgur.com/rSBAMnF.png)

既然说到了引用数据类型，就一定可以发生引用传递，而现在的引用传递的本质也一定是：
> 同一块堆内存的空间可以被不同的栈内存所指向。

**范例** 定义一个程序：

	public class ArrayDemo {
	
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			int data [] = new int [3];
			int temp [] = null;
			data[0] = 10;//第1个元素
			data[1] = 20;//第2个元素
			data[2] = 30;//第3个元素
			//如果要发生引用传递，不要出现[]
			temp = data;//int temp []  = data
			temp[0] = 99; // 修改数据
			for (int x = 0 ; x <data.length ;x++) {
				System.out.println(data[x]);
			}
		}
	}

**console：**

	99
	20
	30


![](https://i.imgur.com/1yfqlZF.png)

引用传递的分析都是类似的：同一块堆内存被不同的栈内存所指向。


## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course11)
