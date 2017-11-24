## [上一页](course13)

## 6.6 Java对数组的支持

在Java给出的类库中也提供有对于数组进行操作的方法：

- 数组排序：java.util.Arrays.sort（数组名称）；

**范例** 数组排序：

	public class ArrayDemo {
	
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			int data [] = new int [] {6,12,3,1,34};
			char arr [] = new char[] {'X','C','A'};
			
			java.util.Arrays.sort(data);
			java.util.Arrays.sort(arr);
			
			printArray(data);
			printArray(arr);
		}
		//定义一个专门进行数组输出的方法
		public static void printArray(int temp []) {
			for(int x = 0; x < temp.length ;x++) {
				System.out.println(temp[x] + "、");
			}
			System.out.println();
		}
		public static void printArray(char temp []) {
			for(int x = 0; x < temp.length ;x++) {
				System.out.println(temp[x] + "、");
			}
			
		}
	}


**console：**

	1、
	3、
	6、
	12、
	34、
	
	A、
	C、
	X、

只要是基本数据类型的数组，Arrays.sort（）都可以进行排序处理，没有需求都是默认升序。

- 数组拷贝：将数组的部分内容替换掉另外一个数组的部分内容；

		方法（加工）：System.arraycopy（源数组名称，源数组开始点，目标数组名称，目标数组开始点，拷贝长度）；

**范例** 实现数组拷贝：
	
	- 源数组A：1、2、3、4、5、6、7、8、9；

	- 源数组A：11、22、33、44、55、66、77、88、99；

	- 替换后的数组A：1、55、66、77、5、6、7、8、9；

	public class ArrayDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			int dataA [] = new int [] {1,2,3,4,5,6,7,8,9};
			int dataB [] = new int [] {11,22,33,44,55,66,77,88,99};
			
			System.arraycopy(dataB, 4, dataA, 1, 3);
			printArray(dataA);
		}
		//定义一个专门进行数组输出的方法
		public static void printArray(int temp []) {
			for(int x = 0; x < temp.length ;x++) {
				System.out.println(temp[x] + "、");
			}
			System.out.println();
		}
	}

**console：**

1、
55、
66、
77、
5、
6、
7、
8、
9、

这些基本的数据操作只能够作为逻辑练习，开发过程很少涉及。

## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course15)
