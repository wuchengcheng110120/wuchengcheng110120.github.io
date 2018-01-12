## [上一页](course50)
## Arrays类

java.lang.Object

	java.util.Arrays


数组排序时使用过Arrays类：

在这个类中实现了二分查找法： public static int binarySearch(double[] a,
                               int fromIndex,
                               int toIndex,
                               double key)

数组拷贝操作：public static int[] copyOf(int[] original,
                           int newLength)

数组比较（顺序相同）：public static boolean equals(int[] a,
                             int[] a2)

数组填充：public static void fill(int[] a,
                        int val)

数组排序：public static void sort(int[] a)

数字变为字符串输出;public static String toString(int[] a)

**范例** 观察Arrays类：

	package cn.mldn.demo;
	
	import java.util.Arrays;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			int dataA[] = new int[] {1,2,3,4,5};
			int dataB[] = new int[] {1,2,3,4,5};
			System.out.println(Arrays.toString(dataA));
			System.out.println(Arrays.equals(dataA, dataB));
			System.out.println(Arrays.binarySearch(dataA, 5));
		}
	}
**console：**

	[1, 2, 3, 4, 5]
	true
	4

实际开发中意义不大。



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course52)
