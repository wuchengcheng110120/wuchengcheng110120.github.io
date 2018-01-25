## [上一页](course86)
##  【第11个代码模型】打印流（格式化文本信息）

C语言中的printf()函数，在打印的时候可以使用一些占位符，例如：字符串（%s）、数字（%d）、小数（%m.nf）、字符（%c）等。从JDK1.5开始，PrintStream类中也追加了同样的操作方式，使用的是printf()方法

- 格式化输出： public PrintStream printf(String format,
                          Object... args)

**范例** 观察格式化输出：

	import java.io.File;
	import java.io.FileOutputStream;
	import java.io.PrintWriter;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			String name = "小鱼籽";
			int age = 20;
			double salary = -100000.8992378923;
			PrintWriter pu = new PrintWriter(new FileOutputStream(new File("d:" + File.separator + "info.txt")));
			pu.printf("姓名： %s, 年龄：%d, 工资：%8.2f", name,age,salary);
			pu.close();
		}
	}

同时在String类里面也追加了一个格式化字符串的方法：

- 格式化字符串：public static String format(String format,
                            Object... args)

	public class TestDemo {
		public static void main(String[] args) throws Exception {
			String name = "小鱼籽";
			int age = 20;
			double salary = -100000.8992378923;
			String str = String.format("姓名： %s, 年龄：%d, 工资：%8.2f",  name,age,salary);
			System.out.println(str);
		}
	}
**console：**

	姓名： 小鱼籽, 年龄：20, 工资：-100000.90

开发中一定会使用打印流，有些开发中会自动包装打印流，以后讲解AJAX处理的时候都是打印流支撑的。

不能做二进制输出。



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course88)
