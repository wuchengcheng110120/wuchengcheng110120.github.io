## [上一页](course05)
## Java基础新特性（foreach 输出）

增强型for循环：foreach；

**范例** 原始数组通过for循环输出：

	public class TestDemo {
		public static void main(String[] args) {
			int data[] = new int[] { 1, 2, 3, 4, 5, };//原始数组
			for (int i = 0; i < data.length; i++) {
				System.out.println(data[i]);//通过循环来控制角标
			}
		}
	}

但是从JDK1.5之后对于for循环的使用有了一种新的格式：

for（数据类型 临时变量 ： 数组）{
	
	//循环次数为数组长度，而每一次循环都会顺序取出数组的一个元素赋值给临时变量
}

即：在for循环里面没有必要再去使用索引取数据了。

**范例** 使用增强型for循环：

	public class TestDemo {
		public static void main(String[] args) {
			int data[] = new int[] { 1, 2, 3, 4, 5, };//原始数组
			for (int i : data) { //将数组中的每一个元素设置给i
				System.out.println(data[i]);//这种循环避免了角标的问题
			}
		}
	}

通过此方式可以避免数组越界问题，但是这种数组操作只适合于简单处理模式。


## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course07)
