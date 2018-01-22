## [上一页](course67)
##  File文件操作类（File类基本操作）

如果想学好IO,必须学好抽象类，IO的操作部分重点掌握两个代码模型。整个IO的核心组成就是五个类（File类、OutputStream、InputStream、Writer、Reader），一个接口（Serializable）。

在java.io包中，File类是唯一一个与文件本身操作（文件的创建、删除和取得文件信息等等）有关的程序类。

java.io.File是一个普通的类，所以这个类的使用直接产生实例化对象即可。

如果要实例化对象则需要使用两个构造方法：

- 构造方法一： File(String pathname)

- 构造方法二： File(File parent, String child)，设置父路径和子文件

如果想要进行文件的基本操作，可以使用File类中的如下方法：

- 创建一个新文件： public boolean createNewFile()
                      throws IOException 

**范例** 创建文件：

	import java.io.File;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			File file = new File("d:\\hello.text");
			file.createNewFile();
		}
	}
创建文件本身，对于其内容并不负责，文件内容为空；

- 删除文件：public boolean delete()

- 判断文件是否存在：public boolean exists()

**范例** 编写一个文件的基本操作：

如果文件不存在则创建一个文件，如果文件存在则进行删除；

	import java.io.File;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			File file = new File("d:\\hello.text");
			if (file.exists()) {//文件存在
				file.delete();//文件删除
			}else {
				file.createNewFile();//创建新文件
			}
		}
	}

以上实现了文件的最简单的处理操作，但是此时的代码之中存在有两个问题：

- 对于项目的开发只有Windows（Macbook）最好用，但是在实际的项目部署环境都要求在Unix、Linux之中；

这个时候路径的问题就很麻烦了，Windows使用的是“\”,而Unix下使用的都是“/”,所以在使用路径分隔符的时候都会采用File类的一个常量来描述：public static final String separator

	//由操作系统所在的JVM决定最终的separator是什么内容
		File file = new File("d:"+File.separator+"hello.text");

- 因为在Java中要进行文件处理需要本地操作系统的支持，这之中如果操作的是同名文件，就有可能出现延迟的问题。

![](https://s1.ax1x.com/2018/01/22/p42k6S.png)

避免重名操作就可以解决此问题。




## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course69)
