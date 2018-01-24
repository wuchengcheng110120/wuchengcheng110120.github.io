## [上一页](course76)
##  字节流与字符流（字符输入流：Reader）

Reader依然也是一个抽象类，如果文件读取使用FileReader类：


	public abstract class Reader
	extends Object
	implements Readable, Closeable

Writer和Reader从JDK1.1开始出现；

![](https://s1.ax1x.com/2018/01/24/poHMbn.png)

Reader类中没有方法可以直接进行读取字符串，这个时候只能够按照原始的方式，通过数组的方式进行读取操作；

**范例** 通过Reader进行读取：

	import java.io.File;
	import java.io.FileReader;
	import java.io.Reader;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			File file  = new File("d:" + File.separator + "hello.txt");//1、通过File类定义文件路径
			if (file.exists()) {
				Reader in = new FileReader(file);
				char data[] = new char[1024];
				int len = in.read(data);
				System.out.println(new String(data,0,len));
				in.close();
			}
		}	
	}
**console：**

	世界和平
字符流在进行单个数据的读取要比字节流更加方便的处理中文操作。


## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course78)
