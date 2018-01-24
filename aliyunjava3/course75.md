## [上一页](course74)
##  字节流与字符流（字节输入流：InputStream）

利用OutputStream实现了程序输出内容到文件的处理，那么下面就需要通过程序读取文件内容，就要使用到InputStream类，这个类的定义如下：

public abstract class InputStream
extends Object
implements Closeable

InputStream类只实现了Closeable接口，在InputStream类里面提供有如下的方法：

- 读取数据到字节数组内： public int read(byte[] b)
         throws IOException
	
	|- 返回数据的读取个数，如果开辟数组大小大于读取数据的大小，则返回的就是读取个数
	
	|- 如果现在要读取的数据大于开辟数组，则返回的是开辟数组的长度（len）

	|- 如果没有数据，返回-1

- 读取数据到部分字节数组之中：public int read(byte[] b,
                int off,
                int len)
         throws IOException
	
	|- 读取部分数据，如果没读取满则返回读取个数，读取满则返回数组长度（len），没有数据返回-1

- 读取单个字节： public abstract int read()
                  throws IOException

	|- 每次读取一个字节内容个，没有数据返回-1

InputStream是一个抽象类，如果要对文件进行处理则肯定要使用FileInputStream类完成。

![](https://s1.ax1x.com/2018/01/24/pooBUf.png)

**范例** 实现文件信息的读取：
	
	import java.io.File;
	import java.io.FileInputStream;
	import java.io.InputStream;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			File file  = new File("d:" + File.separator + "hello.txt");//1、通过File类定义文件路径
			if (file.exists()) {//必须保证文件存在才能进行读取处理
				InputStream input = new FileInputStream(file);
				byte data[] = new byte[1024];//每次可以读取的最大数量
				int len = input.read(data);//读取数据到数组
				System.out.println("读取内容【"+ new String(data,0,len)+"】");
				input.close();
			}
		}	
	}
**console：**

	读取内容【www.mldn.cnwww.mldn.cnwww.mldn.cnwww.mldn.cnwww.mldn.cnwww.mldn.cn
	www.mldn.cn
	www.mldn.cn
	www.mldn.cn
	www.mldn.cn
	www.mldn.cn
	www.mldn.cn
	www.mldn.cn
	www.mldn.cn
	www.mldn.cn
	www.mldn.cn
	www.mldn.cn
	wwwwww】

整个流程可以发现，整个OutputStream和InputStream类的使用形式上是非常类似的。

每次程序读取大小限制读取速度，和硬件软件都相关（U盘读取，网盘下载等）；


## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course76)
