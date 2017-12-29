## [上一页](course06)
## Java基础新特性（静态导入）

首先看如下一个简单程序， 提供有static方法：

**范例**  MyMath类：

	package cn.mldn.util;
	
	public class MyMath {
		public static int add(int x, int y) {
			return x + y;
		}
		public static int sub(int x, int y) {
			return x - y;
		}
	}

两个方法都是static方法，原来的使用方法是导入MyMath类而后，利用MyMath类来调用全部的static方法；

**范例** 使用MyMath类：

	package cn.mldn.demo;
	
	import cn.mldn.util.MyMath;
	
	public class TestDemo {
		public static void main(String[] args) {
			System.out.println(MyMath.add(10, 20));
			System.out.println(MyMath.sub(30, 10));
		}
	}
**console：**
	30
	20

方法的最初调用，而从JDK1.5开始，如果发现类中的方法全部都是static方法，则可以直接将这个类的方法导入进来，这样就好比在主方法直接定义的方法，可以被主方法直接调用。

	package cn.mldn.demo;
	
	import static cn.mldn.util.MyMath.*;//静态导入
	
	public class TestDemo {
		public static void main(String[] args) {
			System.out.println(add(10, 20));
			System.out.println(sub(30, 10));
		}
	}

很少用到静态导入，能看懂即可；

新特性中，可变参数和foreach使用的相对更多一些；

## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course08)
