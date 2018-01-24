## [上一页](course78)
##  字节流与字符流（转换流）


现在为止已经知道了两类数据流：字节流和字符流，实际上这两类流也可以互相转换处理：

- OutputStreamWriter： 将字节输出流变为字符输出流

	|-Writer对于文字的输出要比OutputStream方便，可以直接输出字符串

- InputStreamReader： 将字节输入流变为字符输入流

	|-InputStream读取的是字节不方便中文处理

如果想要发现以上两个类的意义，则首先必须来看两个类的继承关系：

- public class OutputStreamWriter
	extends Writer

		构造方法	public OutputStreamWriter(OutputStream out)

- public class InputStreamReader
extends Reader

		构造方法 public InputStreamReader(InputStream in)


**范例** 转换流：

	import java.io.File;
	import java.io.FileOutputStream;
	import java.io.OutputStream;
	import java.io.OutputStreamWriter;
	import java.io.Writer;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			File file  = new File("d:" + File.separator + "hello.txt");//1、通过File类定义文件路径
			if(!file.getParentFile().exists()) {
				file.getParentFile().mkdirs();
			}
			OutputStream output = new FileOutputStream(file);
			Writer out = new OutputStreamWriter(output);
			out.write("helloworld!");
			out.close();
		}	
	}

这种操作只需要知道即可，主要用来分析FileOutputStream、FileInputStream、FileWriter、FileReader的继承结构；

![](https://s1.ax1x.com/2018/01/24/poLdbj.png)

从继承关系上来看，字符流的处理的处理的确是经过转换后得来的


## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course80)
