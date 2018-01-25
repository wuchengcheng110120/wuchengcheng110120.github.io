## [上一页](course90)
##  【第12个代码模型】Scanner类

打印流解决的是OutputStream的缺陷，BufferedReader解决的是InputStream的缺陷，而java.util.Scanner解决的是BufferedReader类的缺陷（替换了BufferedReader类）。

Scanner是一个专门进行输入流处理的程序类，利用这个类可以方便的处理各种数据类型，同时也可以直接结合正则表达式进行各项处理，在这个类中我们主要关注以下的几个方法：

- 判断是否有指定类型的数据： public boolean hasNextXxx()	【hasNextDouble()、	hasNextInt()等】

- 取得指定类型的数据： public 数据类型 nextXxx()【nextDouble()、	nextInt()等】

- 用正则来定义分隔符： public Scanner useDelimiter(String pattern)

- 构造方法： public Scanner(InputStream source)；

**范例** 使用Scanner实现数据的输入：

	import java.util.Scanner;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			Scanner scan = new Scanner(System.in);
			System.out.print("请输入数据：");
			if (scan.hasNext()) {//有输入内容,不判断空字符串
				System.out.println("【ECHO】 输入内容为：  " + scan.next());
			}
			scan.close();
		}
	}
**console：**

	请输入数据：hello
	【ECHO】 输入内容为：  hello

使用Scanner可以接收其他类型的数据，并且帮助用户减少转型的处理；

**范例** 接受其他类型数据

	import java.util.Scanner;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			Scanner scan = new Scanner(System.in);
			System.out.print("请输入年龄：");
			if (scan.hasNextInt()) {//有输入内容,不判断空字符串
				int age = scan.nextInt();
				System.out.println("【ECHO】 输入内容为：  " + age);
			}else {
				System.out.println("ERROR: 输入的不是数字！" );
			}
			scan.close();
		}
	}
**console：**

	请输入年龄：hello
	ERROR: 输入的不是数字！

	请输入年龄：13
	【ECHO】 输入内容为：  13

最为重要的是Scanner可以对接收的数据类型使用正则表达式进行判断。

**范例** 利用正则进行判断：

	import java.util.Scanner;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			Scanner scan = new Scanner(System.in);
			System.out.print("请输入生日：");
			if (scan.hasNext("\\d{4}-\\d{2}-\\d{2}")) {
				String birthday = scan.next();
				System.out.println("【ECHO】" + birthday);
			}else {
				System.out.println("ERROR:输入格式不对！");
			}
			scan.close();
		}
	}
但是以上的操作在开发之中基本上是不会出现的，因为不会让用户从命令行程序进行数据输入操作。

使用Scanner本身能够接收一个InputStream类的对象，那么也就意味着可以接收任意的输入流，例如：文件输入流；

	import java.io.File;
	import java.io.FileInputStream;
	import java.util.Scanner;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			Scanner scan = new Scanner(new FileInputStream(new File("d:" + File.separator + "info.txt")));
			scan.useDelimiter("\n");
			while (scan.hasNext()) {
				System.out.println(scan.next());
			}
			scan.close();
		}
	}

Scanner完美的替代了BufferedReader，而且更好的实现了InputStream的操作。以后除了二进制文件的copy之外，对于程序信息的输出都使用打印流，程序信息的输入都使用Scanner。



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course92)
