## [上一页](course8)


## 6.1 数组的定义与使用（数组基本概念）

假设要定义100个变量，如果按照之前的做法定义结构如下：
	
	i1,i2...i100;

但是这个时候如果按照此类方式定义就会非常麻烦，因为这些变量彼此之间没有任何关联，如果此时要求输出100个变量的内容，就需要大量的输出语句。

其实所谓的数组指的就是一组相关类型的变量的集合，并且这些变量可以按照统一的方式进行操作。数组本身属于引用数据类型，又会涉及到内存分配，而数组的定义语法有如下两类。

- 数组的动态初始化：
	
		|- 声明并开辟数组：

				数据类型 [] 数组名称 =  new 数据类型 [长度];
				
				数据类型 数组名称 [] =  new 数据类型 [长度];

 		
		|- 分步进行数组空间开辟（实例化）：
				
				声明数组：    

						数据类型 数组名称 [] = null;
		
						数据类型 [] 数组名称 = null;

				开辟数组空间：

						数组名称 = new 数据类型[长度];


当数组开辟空间之后，就可以采用如下的方式进行操作：

- 数组的访问通过索引完成，即：“数组名称[索引]”，但是需要注意的是，数组的索引从0开始，所以可以索引的范围就是0~数组长度-1，例如：先开开辟了3个空间的数组，所以可以使用的索引是0、1、2，如果此时数组访问的时候超过了数组的索引范围，则会产生“ArrayIndexOutOfBoundsException”异常信息；

- 当数组采用动态初始化开辟空间之后，数组里面的每一个元素都是该数组对应类型的默认值；

- 数组本身是一个有序的集合，所以对于数组的内容操作往往会采用循环的模式完成，数组是一个有限的数据集合，所以应该使用for循环；

- 在java中提供有一种动态取得数组长度的方法：数组名称.length ；

**范例** 数组越界：


	public class ArrayDemo {
	
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			int data [] = new int [3];//开辟了一个长度为3的数组
			System.out.println(data[0]);
			System.out.println(data[1]);
			System.out.println(data[2]);
			System.out.println(data[3]);
		}
	
	}

**console：** 

	0
	0
	0
	Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: 3
		at bznoc171118.ArrayDemo.main(ArrayDemo.java:13)


**范例** 数组定义和使用：

	public class ArrayDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			int data [] = new int [3];//开辟了一个长度为3的数组
			System.out.println(data.length);
			data[0] = 10;//第1个元素
			data[1] = 20;//第2个元素
			data[2] = 30;//第3个元素
			for(int  x = 0; x < data.length; x++) {
				System.out.println(data[x]);//通过循环控制索引
			}
		}
	}

**console：** 

	3
	10
	20
	30

数组本身除了声明并开辟空间之外还有另外一种开辟空间的模式。

**范例** 采用分步模式开辟数组空间：

	public class ArrayDemo {
	
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			int data [] = null;
			data = new int [3];					//开辟了一个长度为3的数组
			System.out.println(data.length);
			data[0] = 10;//第1个元素
			data[1] = 20;//第2个元素
			data[2] = 30;//第3个元素
			for(int  x = 0; x < data.length; x++) {
				System.out.println(data[x]);//通过循环控制索引
			}
		}
	}

**console：** 

	3
	10
	20
	30

但是千万要记住，数组属于引用数据类型，所以数组在使用之前一定要开辟空间（实例化），如果使用了没有开辟空间的数组一定会出现*NullPointerException*异常

**范例** 使用没有开辟空间的数组：

	public class ArrayDemo {
	
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			int data [] = null;
			System.out.println(data.length);
			data[0] = 10;//第1个元素
			data[1] = 20;//第2个元素
			data[2] = 30;//第3个元素
			for(int  x = 0; x < data.length; x++) {
				System.out.println(data[x]);//通过循环控制索引
			}
		}
	}

**console：** 

	Exception in thread "main" java.lang.NullPointerException
	at bznoc171118.ArrayDemo.main(ArrayDemo.java:10)

这一原则和之前讲解的对象操作是完全相同的，都是引用数据类型采用的模式。

数组在开发之中一定会使用，但像以下讲解的时候这么用的数组少了，在以后的实际开发之中，会更多的使用数组概念，而直接使用数组99%情况下都只是做一个for循环的输出。


## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course10)

