## [上一页](course77)
##  字节流与字符流（字节流与字符流区别）

通过分析可以发现，使用字节流和字符流在代码的操作上区别不大，但是如果从实际的使用来将，字节流是优先考虑的，只有在处理中文的时候才会使用到字符流。因为所有的字符都需要进行内存缓冲

![](https://s1.ax1x.com/2018/01/24/pobTT1.png)

读数据需要缓冲，写数据同样需要；

如果在字符流操作的时候没有进行刷新就可能在缓存之中，必须强制刷新才能得到完整的数据，flush()方法执行

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
			out.flush();//强制清空缓冲内容
		}	
	}

在以后进行IO处理的时候，如果处理的是图片、音乐、文字都可以使用字节流，只有处理中文的时候才会优先考虑字符流。


## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course79)
