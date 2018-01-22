## [上一页](course70)
##  File文件操作类（综合案例：目录列表）

虽然File类本身提供有listFiles()方法，但是这个方法本身只能够列出本目录中第一级的信息，如果要求列出目录中所有级的信息，则就必须自己来实现处理，这种操作就必须使用递归的模式来完成了。

**范例** 实现该操作：

	import java.io.File;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			File file = new File("d:" + File.separator + "hello" + File.separator);//要操作的文件
			listDir(file);
		}
		/**
		 * 列出指定目录的全部子目录信息
		 * @param file
		 */
		public static void listDir(File file) {
			if (file.isDirectory()) {//现在给定的file是目录
				File result [] = file.listFiles();//继续列出子目录中的内容
				if(result != null) {
					for (int i = 0; i < result.length; i++) {
						listDir(result[i]);// 继续列出
					}
				}
			}
			System.out.println(file);//直接输出
		}		
	}
**console：**

	d:\hello\abc\hello.txt
	d:\hello\abc
	d:\hello\hello.txt
	d:\hello

**线程阻塞问题**

现在的所有代码都是在main线程下进行的，如果列出的操作不完成对于main中后续的执行将无法完成，也就是说这种耗时的操作让我们的主线程暂时出现了阻塞，让后续代码无法正常执行完毕，所以此时如果不想让阻塞产生，那么最好再产生一个新的线程进行处理

	public static void main(String[] args) throws Exception {
			new Thread(()->{
				File file = new File("d:" + File.separator + "hello" + File.separator);//要操作的文件
				listDir(file);
			},"列出线程").start();
			System.out.println("开始进行文件的信息列出...");
	}

上述操作如果将listDir()中列出变为删除就可以成为一个恶意程序了。

如果要在项目中追加这类代码，最笨的人是直接写在程序里面，也可以将此类代码放在开发工具包中。



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course72)
