## [上一页](course81)
##  字符编码（乱码产生原因）

那么既然清楚常用的编码，那么下面就可以观察一下乱码的产生，如果想要观察出乱码，首先必须知道当前操作系统默认支持的编码是什么（Java的默认编码）。

**范例** 读取Java运行属性：

	public class TestDemo {
		public static void main(String[] args) throws Exception {
			System.getProperties().list(System.out);
		}	
	}

如果现在本地系统使用的是GBK或者UTF-8编码，那么保存中文的时候就会选择默认使用的编码，如果强制转换，就会出现乱码。

	import java.io.File;
	import java.io.FileOutputStream;
	import java.io.OutputStream;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			OutputStream output = new FileOutputStream(new File("D:" + File.separator + "info.txt"));
			output.write("世界你好啊！".getBytes("ISO8859-1"));
			output.close();
		}	
	}
**console：**

	？？？？？？

乱码的本质：编码和解码的不同意造成的问题。

以后最常使用的就是UTF-8;



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course83)
