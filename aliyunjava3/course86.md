## [上一页](course85)
##  【第11个代码模型】打印流（使用系统打印流）

打印流有字节打印流：PrintStream、字符打印流：PrintWriter，以后使用PrintWriter的几率挺高的，但是这两者的使用形式是相同的。首先来观察这两个类的继承结构与构造方法：

- PrintStream类：

		|-java.lang.Object
			|-java.io.OutputStream
				|-java.io.FilterOutputStream
					|-java.io.PrintStream

继承结构：

		public class PrintStream
		extends FilterOutputStream
		implements Appendable, Closeable

public PrintStream(OutputStream out)

- PrintWriter类：

		|-java.lang.Object
			|-java.io.Writer
				|-java.io.PrintWriter
继承结构：

	public class PrintWriter
	extends Writer

public PrintWriter(OutputStream out)

![](http://ww4.sinaimg.cn/large/0060lm7Tly1fnswlfxkqpj30va0higtq.jpg)

此时设计模式非常像代理模式，但是代理设计模式有以下的特点：

- 代理是以接口为使用原则的设计模式；

- 最后用户可以调用的方法一定是接口所定义的方法；

打印流的设计属于装饰设计模式。装饰设计模式，核心依然是某一个类的功能，但是为了得到更好的操作效果，让其支持的功能更多一些。

**范例** 使用打印流：

	import java.io.File;
	import java.io.FileOutputStream;
	import java.io.PrintWriter;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			PrintWriter pu = new PrintWriter(new FileOutputStream(new File("d:" + File.separator + "info.txt")));
			pu.print("姓名：");
			pu.println("啊于！");
			pu.println(1 + 10);
			pu.println(1.2 + 10.3);
			pu.close();
		}
	}

以后的开发之中一定会用到打印流。

## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course87)
