## [上一页](course79)
##  字节流与字符流（【第10个代码模型】综合案例：文件拷贝）

在windows下有一个copy命令，该命令使用格式：copy 源文件路径 目标文件路径；

而现在希望通过程序完成这样的操作命令，也就是说建立一个copy程序类通过初始化参数接收源文件路径和目标文件路径。

实现分析：

- 要实现数据拷贝，肯定要通过流的模式来完成，对于流有两类：字节流和字符流。由于要拷贝的内容不一定是文字数据，也有可能是二进制的数据，所以用字节流比较好

- 在进行拷贝的时候需要确定拷贝模式：

	|- 1、在程序中开辟数组，这个数组的长度为文件的长度，所有的数据一次性读取到该数组之中，随后进行输出保存

	|- 2、采用边读边写的方式完成；

**范例** 初期模型：

	import java.io.File;
	import java.io.FileInputStream;
	import java.io.FileOutputStream;
	import java.io.IOException;
	import java.io.InputStream;
	import java.io.OutputStream;
	
	/**
	 * 建立一个专门负责文件拷贝处理的类，该类有如下功能：<br>
	 * 1、需要判断拷贝的源文件是否存在
	 * 2、需要判断目标文件的父路径是否存在，如果不存在则应该创建；
	 * 3、需要进行文件拷贝操作的处理。
	 * @author mldn
	 *
	 */
	class CopyUtil{//这个类不需要保存呢任何的属性，所以建议将构造方法私有化，使用static方法
		private CopyUtil(){}//将构造方法私有化
		/**
		 * 判断要拷贝的路径是否存在
		 * @param path 输入的源路径信息
		 * @return 如果该路径真实存在返回true，否则返回false
		 */
		public static boolean fileExists(String path) {
			return new File(path).exists();
		}
		/**
		 * 根据传入的路径来判断其父路径是否存在，如果不存在则创建
		 * @param path 需要创建的路径，通过此路径创建父路径
		 */
		public static void createDir(String path) {
			File file  = new File(path);
			if (!file.getParentFile().exists()) {//如果路径不存在
				file.getParentFile().mkdirs();//创建路径
			}
		}
		/**
		 * 实现文件拷贝处理
		 * @param srcPath 源文件路径
		 * @param desPath 目标文件路径
		 * @return 拷贝完成返回true，否则返回false
		 */
		public static boolean copy(String srcPath, String desPath) {	
			boolean flag =false;
			File inFile = new File(srcPath);
			File outFile = new File(desPath);
			InputStream input = null;
			OutputStream output = null;
			try {
				input = new FileInputStream(inFile);
				output = new FileOutputStream(outFile);
				copyHandle(input, output);//完成文件拷贝处理
				flag =true;
			}catch(IOException e) {
				flag = false;
			}finally {
				try {
					input.close();
					output.close();
				}catch(IOException e) {}
			}
			return flag;
		}
		/**
		 * 实现文件的具体拷贝操作
		 * @param input 输入流对象
		 * @param output 输出流对象
		 * @throws IOException
		 */
		private static void copyHandle(InputStream input, OutputStream output) throws IOException {
			long start  =System.currentTimeMillis();
			//InputStream有一个读取单个字节的方法 int read()
			//OutputStream有一个输出单个字节的方法 void write(int data)
			int temp  = 0;
			do {
				temp = input.read();//读取单个字节数据
				output.write(temp); //通过输出流输出
			}while(temp != -1);
			long end  = System.currentTimeMillis();
			System.out.println("【拷贝文件所花的时间】" + (end-start));
		}
	}
	
	public class Copy {
		public static void main(String[] args) {
			if (args.length != 2) {//参数不是两个
				System.out.println("错误的执行方式，命令调用：java Copy 源文件路径 目标文件路径");
				System.exit(1);
			}
			//必须判断要拷贝的源文件的路径是否存在
			if (CopyUtil.fileExists(args[0])) {
				CopyUtil.createDir(args[1]);//创建目标的父目录
				System.out.println(CopyUtil.copy(args[0], args[1])? "文件拷贝成功":"文件拷贝失败");
			}else {
				System.out.println("对不起，源文件不存在，无法完成拷贝操作！");
			}
		}
	}

![](https://s1.ax1x.com/2018/01/24/pTCmFg.png)

这个时候的确是执行了，但是这个代码有两个问题：

- 在开发中尽量不要去使用do...while，尽量去使用while循环

- 拷贝速度堪忧。

**范例**解决do...while问题：

		//1、temp = input.read(), 表示读取输入流中的一个字节；
		//2、(temp = input.read()) != -1, 判断这个读取后的字节（保存temp）是否为-1，如果不是表示有内容
		while((temp =input.read()) != -1) {
			output.write(temp);
		}

以上的方式还是针对一个字节的模式完成的，实际上如果文件太大，这种做法一定不可取。

**范例** 解决读取慢的问题：

需要加大缓冲，也就是一次读取多个字节数据，那么就要开辟一个字节数组。

![](https://s1.ax1x.com/2018/01/24/pTP4C4.png)

	/**
	 * 实现文件的具体拷贝操作
	 * @param input 输入流对象
	 * @param output 输出流对象
	 * @throws IOException
	 */
	private static void copyHandle(InputStream input, OutputStream output) throws IOException {
		long start  =System.currentTimeMillis();
		//InputStream有一个读取单个字节的方法 int read()
		//OutputStream有一个输出单个字节的方法 void write(int data)
		int temp  = 0;
		byte data[] = new byte[2048];
		//1、temp = input.read(data), 表示读取输入流中的字节数组，而后返回数据读取个数；
		//2、(temp = input.read()) != -1, 判断这个读取后的字节（保存temp）是否为-1，如果不是表示有内容
		while((temp =input.read(data)) != -1) {
			output.write(temp);//输出部分数组
		}
		long end  = System.currentTimeMillis();
		System.out.println("【拷贝文件所花的时间】" + (end-start));
	}

这个程序最为核心的就是以上代码。这也是以后使用最多的形式

如果要求处理的数据都在InputStream中要求输出就采用以上模型。



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course81)
