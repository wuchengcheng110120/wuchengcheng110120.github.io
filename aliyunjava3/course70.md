## [上一页](course69)
##  File文件操作类（取得文件信息）

在File类中有一系列取得文件数据信息的操作方法：

- 判断路径是否是文件：public boolean isFile()；

- 判断路径是否是目录：public boolean isDirectory()；

- 取得文件大小（字节）： public long length()；

- 最后一次修改日期： public long lastModified()

**范例** 取得文件信息：

	import java.io.File;
	import java.text.SimpleDateFormat;
	import java.util.Date;
	
	
	class MyMath{
		public static double round(double num, int scale) {
			return Math.round(num * Math.pow(10, scale) /Math.pow(10, scale) );
		}
	}
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			File file = new File("d:" + File.separator + "my.jpg");//要操作的文件
			if (file.exists() && file.isFile()) {//必须保证文件存在才能取得相应的信息
				System.out.println("文件大小" + MyMath.round((file.length()/(double)1024/1024), 2));
				System.out.println("最后一次修改日期：" + new SimpleDateFormat("yyyy-MM-dd HH-mm-ss").format(new Date(file.lastModified())));
			}
		}
	}
**console：**

	文件大小1.0
	最后一次修改日期：2017-11-18 14-54-38

以上的操作都是针对文件进行操作，我们也可以根据目录进行相应信息的取得，那么使用如下的一个方法列出一个目录中的全部组成：

- public File[] listFiles()

**范例** 列出目录中的全部组成：

	import java.io.File;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			File file = new File("d:" + File.separator);//要操作的文件
			if (file.exists() && file.isDirectory()) {
				File result[] = file.listFiles();//列出目录中的内容
				for (int i = 0; i < result.length; i++) {
					System.out.println(result[i]);
				}
			}
		}
	}
**console：**

	d:\dlcache
	d:\download
	d:\drivers

以上的操作可以取得本地文件的相关信息。



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course71)
