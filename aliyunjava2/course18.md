## [上一页](course17)

## 6.10 数组案例：二分法查找

要求在指定的数组中查询一个数据的位置，可能想到的最简单的办法九十数组遍历。

**范例** 数组遍历：

	public class ArrayDemo {
	
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			int data [] = new int [] {1,2,3,4,5,6,7,8,9};
			int search = 7;
			System.out.println(index(data, search));
		}
		public static int index(int arr[], int key) {
			for (int x= 0 ; x<arr.length; x++) {
				if(arr[x] == key) {
					return x;
				}
			}
			return -1;
		}
	}

**console：**

	6

这个算法的时间复杂度是n，所有数组中的数据都需要进行一次遍历，才能确认所需要的查找数据是否存在，如果要想进行更快速的查找方法，最好的做法是进行二分查找（折半查找）。

- 二分查找的前提是数组排序

![](https://i.imgur.com/FsHYEXt.png)

**范例** 实现二分查找（采用递归操作完成）：

	public class ArrayDemo {
	
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			int data [] = new int [] {1,2,3,4,5,6,7,8,9};
			int search = 7;
			System.out.println(binarySearch(data, 0, data.length-1, search));
		}
		public static int binarySearch(int arr[], int from, int to, int key) {
			if(from < to) {
				int mid = (from + to)/2;
				if(arr[mid] == key) {
					return mid;
				}else if(key < arr[mid]) {
					return binarySearch(arr, from, mid-1, key);
				}else if(key > arr[mid]) {
					return binarySearch(arr, mid+1, to, key);
				}
			}
			return -1;
		}
	}

**console：**

	6

二分查找属于数据结构课程范围，属于逻辑范围训练。


## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course19)
