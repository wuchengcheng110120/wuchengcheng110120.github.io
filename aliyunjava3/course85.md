## [上一页](course84)
##  【第11个代码模型】打印流（打印流模型）

打印流主要解决的就是OutputStream的设计缺陷，属于OutputStream的功能加强版。如果操作的不是二进制数据，可能只是想通过程序向终端目标输出一些信息的话，OutputStream并不方便，其缺点有两个：

- 缺点一： 所有的数据必须变为字节数组；

- 缺点二：只支持String ，如果要输出的是int、double等类型就不方便了

打印流的设计主要目的是为了解决OutputStream的设计问题，其本质不可能脱离OutputStream，

**范例** 打印流设计模式：

	import java.io.File;
	import java.io.FileOutputStream;
	import java.io.IOException;
	import java.io.OutputStream;
	
	class PrintUtil{//自己编写一个类，希望这个类可以提供更多的输出支持
		private OutputStream output; //定义一个OutputStream
		public PrintUtil(OutputStream output) {//由外部来决定输出的位置
			this.output = output;
		}
		public void print(String str) {
			try {
				this.output.write(str.getBytes());
			} catch (Exception e) {
				e.printStackTrace();
			}
		}
		public void println(String str) {
			this.print(str + "\r\n");
		}
		public void print(int data) {
			this.print(String.valueOf(data));
		}
		public void println(int data) {
			this.println(String.valueOf(data));
		}
		public void print(double data) {
			this.print(String.valueOf(data));
		}
		public void println(double data) {
			this.println(String.valueOf(data));
		}
		public void close() {
			try {
				this.output.close();
			} catch (IOException e) {
				e.printStackTrace();
			}
		}
	}
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			PrintUtil pu = new PrintUtil(new FileOutputStream(new File("d:" + File.separator + "info.txt")));
			pu.print("姓名：");
			pu.println("啊于！");
			pu.println(1 + 10);
			pu.println(1.2 + 10.3);
			pu.close();
		}
	}

发现经过简单的处理之后，让OutputStream的功能变得强大了，其实本质上就只是对OuputStream类的功能做了一个封装，而这样的操作类是不需要你来提供编写的，因为java里面提供有专门的打印流处理类：PrintStram、PrintWriter



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course86)
