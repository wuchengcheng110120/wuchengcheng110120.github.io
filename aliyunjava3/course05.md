## [上一页](course04)
## Java基础新特性（可变参数）

JDK1.8: Lambda表达式、接口的定义加强；

自动装箱与拆箱、switch对String的判断支持；

要求设计一个方法用于计算任意个数的整数的相加结果：

于是这种的开发需求在最早的时候，只能够通过数组的方式来实现。

**范例** 最初的实现模式：

	package cn.mldn.demo;
	
	public class TestDemo {
		public static void main(String[] args) {
			System.out.println(add(new int[] {1}));
			System.out.println(add(new int[] {1,2,3}));
			System.out.println(add(new int[] {1,2,3,4,5,6,7,8}));
		}	
		/**
		 * 实现任意个数的数据的相加处理操作
		 * @param data 要进行相加操作的数据
		 * @return 返回多个数据的相加结果
		 */
		public static int add(int [] data) {
			int sum =0 ;
			for (int i = 0; i < data.length; i++) {
				sum += data[i];
			}
			return sum;
		}		
	}

**console：**
	
	1
	6
	36

关键设计不在一个数组，而是在任意多个参数，JDK1.5前无法使用，JDK1.5以后，追加了可变参数概念。


public[static][final] 返回值 方法名称（参数类型 ... 参数名称）

这个参数上使用的...实际上就描述了一个数组的结构。

	package cn.mldn.demo;
	
	public class TestDemo {
		public static void main(String[] args) {
			System.out.println(add());//随意传递的内容
			System.out.println(add(1,2,2));
			System.out.println(add(1,2,3,4,5,6,7,8));
		}	
		/**
		 * 实现任意个数的数据的相加处理操作
		 * @param data 要进行相加操作的数据
		 * @return 返回多个数据的相加结果
		 */
		public static int add(int ... data) {//本身还是一个数组
			int sum =0 ;
			for (int i = 0; i < data.length; i++) {
				sum += data[i];
			}
			return sum;
		}
	}


**console：**
	
	0
	5
	36

现阶段可以通过类库观察，原则参数个数不确定随意由用户传递。

注意：如果要传递多类参数，可变参数写在最后；

	package cn.mldn.demo;
	
	public class TestDemo {
		public static void main(String[] args) {
			System.out.println(add(""));//随意传递的内容
			System.out.println(add("hello",1,2,2));
			System.out.println(add("world",1,2,3,4,5,6,7,8));
		}	
		/**
		 * 实现任意个数的数据的相加处理操作
		 * @param data 要进行相加操作的数据
		 * @return 返回多个数据的相加结果
		 */
		public static int add(String msg,int ... data) {//本身还是一个数组
			int sum =0 ;
			for (int i = 0; i < data.length; i++) {
				sum += data[i];
			}
			return sum;
		}		
	}

一个方法只能设置一个可变参数；

## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course06)
