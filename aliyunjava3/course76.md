## [上一页](course75)
##  字节流与字符流（字符输出流：Writer）

Writer类是字符输出流的处理类，这个类的定义如下：

public abstract class Writer
extends Object
implements Appendable, Closeable, Flushable

比字节输出流的OutputStream多了一个Appendable接口。

在Writer类里面也提供有write()的方法,而且该方法接收的类型都是char型的，不过里面有一个直接输出字符串的方法：

- 输入内容： public void write(String str)
           throws IOException

同样是一个抽象类，如果要操作文件，肯定要使用FileWriter子类

**范例** 通过Writer类实现输出：

	import java.io.File;
	import java.io.FileWriter;
	import java.io.Writer;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			File file  = new File("d:" + File.separator + "hello.txt");//1、通过File类定义文件路径
			if(!file.getParentFile().exists()) {
				file.getParentFile().mkdirs();
			}
			String msg = "世界和平";
			Writer out = new FileWriter(file);
			out.write(msg);//直接输出字符串
			out.close();
		}	
	}

代码实现结构和OutputStream非常相似；


## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course77)
