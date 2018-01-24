## [上一页](course82)
##  内存操作流（内存流基本操作）

在之前所有的操作都是针对文件进行的IO处理，那么除了文件之外，IO的操作也可以发生在内存之中，这种流就称为内存操作流。

文件流的操作一定会产生一个文件数据（不管这个文件数据是否被保留。）那么现在的要求是需要发生IO处理，那么又不希望产生文件。这种情况下就可以使用内存作为操作终端

![](http://ww2.sinaimg.cn/large/0060lm7Tly1fnrxtyqqhhj30vh0hh79q.jpg)

在Java中有两类数据流：

- 字节内存流：ByteArrayInputStream、ByteArrayOutputStream

- 字符内存流：CharArrayReader、CharArrayWriter

观察ByteArrayInputStream和ByteArrayOutputStream类中提供的构造方法：

- ByteArrayInputStream构造方法：ByteArrayInputStream(byte[] buf)

- ByteArrayOutputStream构造方法： ByteArrayOutputStream()


![](http://ww4.sinaimg.cn/large/0060lm7Tly1fnry2yx09yj30ve0hkjx7.jpg)

内存输出流的继承关系：

![](http://ww2.sinaimg.cn/large/0060lm7Tly1fnry5mow9hj30ve0hjdlk.jpg)

内存输入流的继承关系：

![](http://ww3.sinaimg.cn/large/0060lm7Tly1fnry802xi2j30vc0hgwjr.jpg)

**范例** 通过内存流实现一个大小写转换的操作：

	import java.io.ByteArrayInputStream;
	import java.io.ByteArrayOutputStream;
	import java.io.InputStream;
	import java.io.OutputStream;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			String msg = "hello world !!!";
			//实例化InputStream类对象，实例化的时候需要将你操作的数据
			//保存到内存之中，最终你读取的就是你设置的内容
			InputStream  input = new ByteArrayInputStream(msg.getBytes());
			OutputStream output = new ByteArrayOutputStream();
			int temp =0;
			while ((temp = input.read()) != -1) {
				output.write(Character.toLowerCase(temp));//每个字节数据进行处理
			}//此时所有的数据都在OutputStream类中
			System.out.println(output);//直接输出对象调用toString()
			input.close();
			output.close();
		}	
	}
**console：**

	hello world !!!

这个时候发生了IO操作，但是没有文件产生，所以可以理解为一个临时文件方式处理。



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course84)
