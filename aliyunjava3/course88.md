## [上一页](course87)
##  System类对IO的支持（系统输出）

学习完了PrintStream、PrintWriter之后我们会发现里面的方法都很熟悉，例如：print()、println(),实际上在之前使用的系统输出就利用了IO流的模式完成。在System类中定义有三个操作的常量：

- 错误输出：public static final PrintStream err

- 标准输入（键盘）：public static final InputStream in

- 标准输出（显示器） public static final PrintStream out

原来之前使用的System.out.print()都属于IO的操作范畴。

系统输出有两个常量：out、err，而且这两个常量所表示的都是PrintStream类的一个对象。从Java的设计本质上来讲这样的两种输出有以下的设计目的：out输出的是希望用户看到的内容、err输出的是希望输出用户不能看见的内容。

这两种输出在实际开发之中都没有用。

	public class TestDemo {
		public static void main(String[] args) throws Exception {
			try {
				Integer.parseInt("abc");
			} catch (Exception e) {
				System.err.println(e);
				System.out.println(e);
			}
		}
	}
**console：**

	java.lang.NumberFormatException: For input string: "abc"
	java.lang.NumberFormatException: For input string: "abc"

System.err也只是作为一个保留的属性提供存在的，唯一可能使用的就是System.out（也基本不会在开发中出现）。但是从另外一个方面来讲。由于System.out属于PrintStream类的实例化对象，而PrintStream又属于OutputStream类的子类，所以可以直接用System.out为OutputStream实例化，那么这个时候的OutputStream输出的位置将变为屏幕。

**范例** 使用System.out为OutputStream实例化：

	import java.io.OutputStream;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			OutputStream out = System.out; //子类实例向上转型
			out.write("世界，和平".getBytes());
		}
	}
**console：**

	世界，和平

抽象类不同的子类针对同一方法有不同的实现，而用户调用的时候核心参考的就是OutputStream。



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course89)
