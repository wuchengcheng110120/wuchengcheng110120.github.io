## [上一页](course11)

## 6.4 二维数组
之前学习的数组只需要一个索引就可以进行访问，这样的数组实际上非常像一个数据行的概念。

索引| 0 | 1 | 2 | 3 | 4 | 5 | 6 | 7
----|----|----|----|----|----|----|----|---
内容| 23 | 23 | 43 | 235 | 235 | 423 | 231 |321
 
现在通过一个索引就可以获得唯一的一个记录，这样的数组简单理解为一位数组，二维数组本质上就是一个行列的集合，想确定某一数据需要行索引和列索引来进行定位。


索引（上行、左列）     | 0 | 2 | 3 | 4 | 5 | 6 
----|----|----|----|----|----|----
0 | 23 | 23 | 43 | 235 | 235 | 423 
1 | 213 |23 | 445 | 53 | 65 | 34
1 | 1 | 2 | 35 | 421 | 63| 98

如果想要确定一个数据则数组使用的结构就是“数组名称[行索引][列索引]”，所以这样的结构就是一个表的结构。

二维数组的定义有两种声明形式：

- 数组的动态初始化： 

		数据类型 对象数组 [][] = new 数据类型[行个数][列个数]；

- 数组的静态初始化：

		数据类型 对象数组 [][] = new 数据类型[][]{
			{值，值，...}，{值，值，...}，{值，值，...}，...
		}；

数组的数组就是二维数组。

**范例** 定义一个二维数组：

	public class ArrayDemo {
			public static void main(String[] args) {
			// TODO Auto-generated method stub
				int data [][] = new int [][] {
					{1,2,3},{4,5},{6,7,8,9}
				};
				//输出时要使用双重循环，外部的循环控制输出行数，内部循环控制输出列数
				for(int x = 0; x < data.length ; x++) {
					for(int y = 0; y < data[x].length;y++) {
						System.out.println("data[" +x+ "][" +y+ "] = " + 
					data[x][y] + "、");
					}
					System.out.println();
				}
			}
	}

**console：**

	data[0][0] = 1、
	data[0][1] = 2、
	data[0][2] = 3、
	
	data[1][0] = 4、
	data[1][1] = 5、
	
	data[2][0] = 6、
	data[2][1] = 7、
	data[2][2] = 8、
	data[2][3] = 9、


开发过程中，二维数组使用频率不高，了解概念即可。


## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course13)