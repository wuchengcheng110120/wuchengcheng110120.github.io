## [上一页](course72)
##  字节流与字符流（字符输出流OutputStream）

如果想用程序进行内容的输出，可以使用java.io.OutputStream类，那么首先来观察这个类的定义结构：

public abstract class OutputStream
extends Object
implements Closeable, Flushable

OutputStream类实现了Closeable、Flushable两个接口，这两个接口中有各自的方法：

- Closeable：public void close()throws IOException；

- Flushable：public void flush()throws IOException；

而在OutputStream类里面实际上还定义有其他方法：

- 将给定的字节内容全部输出： public void write(byte[] b)
           throws IOException

- 将部分的字节内容输出： public void write(byte[] b,
                  int off,
                  int len)
           throws IOException

- 输出单个字节： public abstract void write(int b)
                    throws IOException

但是OutputStream类是一个抽象类，所以按照抽象类的原则来讲，如果要想为父类实例化，那么就需要使用子类。因为方法名称都已经被父类定义好了，所以此处我们关注的主要是子类的构造方法。如果想要进行文件的操作可以使用FileOutPutStream类来处理，这个类的构造:

- 接收File类： public FileOutputStream(File file)
                 throws FileNotFoundException

- 追加内容：public FileOutputStream(File file,
                        boolean append)
                 throws FileNotFoundException

![](http://ww1.sinaimg.cn/large/0060lm7Tly1fnqq1yeernj30vd0hmdo7.jpg)

**范例** 实现文件的内容输出：

	import java.io.File;
	import java.io.FileOutputStream;
	import java.io.OutputStream;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			File file  = new File("d:" + File.separator + "hello.txt");//1、通过File类定义文件路径
			if (!file.getParentFile().exists()) {//必须保证父目录存在
				file.getParentFile().mkdirs();//创建目录
			}
			//2、OutPutStream类是一个抽象类，需要通过子类进行实例化
			OutputStream output = new FileOutputStream(file);//意味着只能够进行文件处理
			//3、进行文件的输出操作
			String msg = "www.mldn.cn";//这个是要求输出的内容
			output.write(msg.getBytes());//将内容变为字节数组
			output.close();
		}	
	}
在进行文件输出的时候所有的文件会自动帮助用户创建，不再需要编写createNewFile()方法手工创建

这个时候程序重复执行，不会出现追加而是覆盖掉之前的，因为默认的状态是覆盖的重复输出，如果需要追加内容，需要更换FileOutputStream类的构造方法。

如果要换行则在字符串的最后追加“\r\n”;

如果要不分输出则更换write()方法；

最常用方法：将部分的字节内容输出： public void write(byte[] b,
                  int off,
                  int len)
           throws IOException

整个输出流程和之前面向对象所学习的操作模式是相通的，唯一的区别是FileOutputStream类里面多了一些文件内容的操作支持。

## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course74)
