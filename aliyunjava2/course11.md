## [上一页](course10)

## 6.3 数组静态初始化

之前的数组定义都有一个明显特点：数组首先先开辟内存空间，而后再使用索引进行内容设置，这种做法叫做动态初始化，而如果希望数组在定义的时候可以同时设置内容，那么就可以采用静态初始化完成。

数组的静态初始化语法一共分为以下两种类型：

简化格式：

	数据类型 数组名称 [] = {值，值，...}；

完整格式：

	数据类型 数组名称 [] = new 数据类型 [] {值，值，...}；

**范例** 采用静态初始化定义数组：

	public class ArrayDemo {
			public static void main(String[] args) {
			// TODO Auto-generated method stub
			int data [] = {1,2,23,4,54,34,123,1234,346,54};
			for (int x = 0 ; x <data.length ;x++) {
				System.out.println(data[x]);
			}
		}
	}

**console：**

	1
	2
	23
	4
	54
	34
	123
	1234
	346
	54

在开发之中，对于静态数组的初始化强烈建议使用完整语法格式，这样可以轻松的使用匿名数组这一概念。

**范例** 匿名数组：

	public class ArrayDemo {
	
		public static void main(String[] args) {
			// TODO Auto-generated method stub
				System.out.println(new int [] {1,2,23,4,54,34,123,1234,346,54}.length);
			}
	}

**console：**

	10

以后使用静态方式定义数组的时候一定要写上完整格式。

数组最大的缺陷：长度固定。


## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course12)
