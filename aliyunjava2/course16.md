## [上一页](course15)

## 6.8 数组案例：数组排序


很多面试题都会出现数组排序的操作形式，但是不要写：java.util.Arrays.sort（数组），

而这种排序以升序为主。

- 基础的排序操作：

![](https://i.imgur.com/pNF3yiV.png)

但是发现最终要进行的循环次数就是：n*（n-1），所以要循环的次数很多，时间复杂度过高。

**范例** 数组冒泡排序实现：

	public class ArrayDemo {
	
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			int data [] = new int [] {9,8,5,6,4,2,1,0,3,7};
			sort(data);
			printArray(data);
			
		
		}
		public static void sort(int arr[]) {
			for (int x=0; x<arr.length; x++) {
				for (int y=0; y<arr.length-x-1; y++) {
					if (arr[y]>arr[y+1]) {
						int temp = arr[y];
						arr[y] = arr[y+1];
						arr[y+1] = temp;
					}
				}
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

	0、1、2、3、4、5、6、7、8、9、
		
  
## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course17)
