## [上一页](course12)

## 6.5 数组与方法互操作

数组是一个引用数据类型，所有的引用数据类型都可以为其设置多个栈内存指向，所以在进行数组操作的时候也可以通过方法进行处理。

**范例** 方法接收数组：

	public class ArrayDemo {
	
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			int data []  = new int []{1,2,3,4,5};
			int temp [] = data; //引用传递
			printArray(temp);
		}
		//定义一个专门进行数组输出的方法
		public static void printArray(int temp []) {
			for(int x = 0; x < temp.length ;x++) {
				System.out.println(temp[x] + "、");
			}
		}
	}

**console：**

	1、
	2、
	3、
	4、
	5、

在方法的参数上由于需要接受一个整形数组，所以就实现了一个最为基础的引用传递操作。

**范例** 方法返回数组：

	public class ArrayDemo {
	
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			int data []  =init();
			printArray(data);
		}
		
		public static int[] init() {
			return new int [] {1,2,3,4,5};
		}
		//定义一个专门进行数组输出的方法
		public static void printArray(int temp []) {
			for(int x = 0; x < temp.length ;x++) {
				System.out.println(temp[x] + "、");
			}
		}
	}

**console：**

	1、
	2、
	3、
	4、
	5、

现在的数组上发生了引用传递，意味着方法接收数组之后也可以对数组内容进行修改。

**范例** 实现数组内容乘二的方法：

	public class ArrayDemo {
	
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			int data []  =init();
			intc(data);//扩大数组中的内容
			printArray(data);
		}
		
		public static void intc(int arr[]) {
			for(int x = 0 ;x < arr.length; x++) {
				arr[x] *= 2;
			}
		}
		
		public static int[] init() {
			return new int [] {1,2,3,4,5};
		}
		//定义一个专门进行数组输出的方法
		public static void printArray(int temp []) {
			for(int x = 0; x < temp.length ;x++) {
				System.out.println(temp[x] + "、");
			}
		}
	}

**console：**

	2、
	4、
	6、
	8、
	10、

![](https://i.imgur.com/UZ2H1LJ.png)

方法的参数传递也是一个堆内存被多个栈内存指向。

## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course14)
