## [上一页](course68)
##  File文件操作类（创建目录）

之前创建的文件都是在根目录下进行的操作，那么如果说现在有目录出现，则以上的代码都无法执行。

**范例** 错误的代码：

	import java.io.File;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			//由操作系统所在的JVM决定最终的separator是什么内容
			File file = new File("d:"+File.separator+"hello"+File.separator+"hello.txt");
			if (file.exists()) {//文件存在
				file.delete();//文件删除
			}else {
				file.createNewFile();//创建新文件
			}
			Thread.sleep(100);
		}
	}
**console：**

	Exception in thread "main" java.io.IOException: 系统找不到指定的路径。
		at java.io.WinNTFileSystem.createFileExclusively(Native Method)
		at java.io.File.createNewFile(Unknown Source)
		at cn.mldn.demo.TestDemo.main(TestDemo.java:12)

因为现在没有父路径所以文件无法找到，那么如何找到父路径呢？在File类中定义有如下的方法：

- 取得父路径： public File getParentFile()

	|- 因为需要进行父目录的创建，所以此处最好取得的是父路径的File类对象；

- 创建目录： public boolean mkdir()

	import java.io.File;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			//由操作系统所在的JVM决定最终的separator是什么内容
			File file = new File("d:"+File.separator+"hello"+File.separator+"abc"+File.separator+"hello.txt");
			if (!file.getParentFile().exists()) {
				file.getParentFile().mkdirs();
			}
			if (file.exists()) {//文件存在
				file.delete();//文件删除
			}else {
				file.createNewFile();//创建新文件
			}
			Thread.sleep(100);
		}
	}

在以后的开发中，父目录的创建判断会经常出现。


## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course70)
