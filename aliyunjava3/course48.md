## [上一页](course47)
## 数字操作类（Math类）

数字操作类指的是针对与数字进行处理，可以使用内置的数学类完成，也可以生成一些随机数。

java.lang.Math类是整个JDK里面唯一一个与数学计算有关的程序类。

这里面提供有一些基础的数学函数。这个类中的所有方法都使用了static进行定义，那么所有的方法都可以通过类名称直接调用，而此类中有一个round（）方法需要特别注意：

- 方法定义： 四舍五入->public static long round(double a)

**范例** 观察round方法：

	public class TestDemo {
		public static void main(String[] args) throws Exception {
			double num = 82389.56789;
			System.out.println(Math.round(num));
		}
	}
**console：**

	82390

round（）默认将小数位直接进位；

**范例** 继续观察round（）的数据处理：

	public class TestDemo {
		public static void main(String[] args) throws Exception {
			System.out.println(Math.round(15.5));
			System.out.println(Math.round(15.51));
			//如果负数小数没大于0.5都不进位
			System.out.println(Math.round(-15.5));
			System.out.println(Math.round(-15.51));
		}
	}
**console：**
	
	16
	16
	-15
	-16

希望可以准确的保存小数位进行处理

	package cn.mldn.demo;
	
	class MyMath{
		/**
		 * 进行数据的四舍五入操作
		 * @param num 表示原始的操作数据
		 * @param scale 表示保留的小数位数
		 * @return 返回已经正确四舍五入后的内容
		 */
		public static double round(double num,int scale) {
			return Math.round(num * Math.pow(10, scale))/Math.pow(10, scale);
		}
	}
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			System.out.println(MyMath.round(1823.2567, 2));
		}
	}
**console：**

	1823.26

这种四舍五入是种最简单的模式。



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course49)
