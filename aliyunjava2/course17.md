## [上一页](course16)

## 6.9 数组案例：数组转置

所谓的数组反转reverse就是首尾交换，实现这样的交换有两种实现思路：

- 思路一：开辟一个新的等长数组，将原数组倒序保存进去。

**范例** 开辟新数组实现：

	public class ArrayDemo {
	
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			int data [] = new int [] {1,2,3,4,5,6,7,8};
			data = reverse(data);
			printArray(data);
			
		
		}
		public static int[] reverse(int arr[]) {
			int temp [] = new int [arr.length] ;
			int foot = 0;//作为数组保存的索引
			for(int x = arr.length-1; x>=0; x--) {
				temp[foot++] = arr[x];
			}
			return temp;
		}
		public static void printArray(int temp[]) {
			for(int x=0; x<temp.length; x++) {
				System.out.print(temp[x] + "、");
			}
			System.out.println();
		}
	}

**console：**

	8、7、6、5、4、3、2、1、

![](https://i.imgur.com/ZYyuvH0.png)

使用此类模式实现的最大问题在于开辟了两块相同的堆内存空间，造成了空间浪费。

- 思路二：在一个数组内完成转换

![](https://i.imgur.com/DBimzHv.png)

![](https://i.imgur.com/U9m2eyG.png)

这种操作只要根据数组长度除2即可

**范例** 在一个数组内完成：

	public class ArrayDemo {
	
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			int data [] = new int [] {1,2,3,4,5,6,7,8,9};
			reverse(data);
			printArray(data);
		}
		
		public static void reverse(int arr[]) {
			int center = arr.length/2;
			int head = 0;
			int tail =arr.length-1;
			for (int x=0; x<center; x++) {
				int temp = arr[head];
				arr[head] = arr[tail];
				arr[tail] = temp;
				head++;
				tail--;
			}
		}
		public static void printArray(int temp[]) {
			for(int x=0; x<temp.length; x++) {
				System.out.print(temp[x] + "、");
			}
			System.out.println();
		}
	}

**console：**

	9、8、7、6、5、4、3、2、1、

如果要进行二维数组的转置，在原数组上操作要求行列相等，否则最好新建数组进行操作。

二维数组转置对角线元素不变，行列数据互换。

![](https://i.imgur.com/3AjVCFF.png)
（图中改：第03次）

**范例** 二维数组转置（保证对角线元素不懂（x==y））：

	public class ArrayDemo {
	
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			int data [][] = new int [][] {{1,2,3},{4,5,6},{7,8,9}};
			reverse(data);
			printArray(data);
		}
		
		public static void reverse(int arr[][]) {
			for (int x=0; x<arr.length; x++) {
				for (int y=x; y<arr[x].length; y++) {
					if(x!=y) {
						int temp = arr[x][y];
						arr[x][y] = arr[y][x];
						arr[y][x] = temp;
					}
				}
			}
		}
		public static void printArray(int temp[][]) {
			for(int x=0; x<temp.length; x++) {
				for(int y=0; y<temp[x].length; y++) {
					System.out.print(temp[x][y] + "、");
				}
				System.out.println();
			}
			System.out.println();
		}
	}

**console：**

	1、4、7、
	2、5、8、
	3、6、9、

逻辑题多练习即可


## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course18)
