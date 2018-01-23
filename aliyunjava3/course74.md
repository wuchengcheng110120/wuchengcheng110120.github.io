## [上一页](course73)
##  字节流与字符流（AutoCloseable自动关闭支持）

从JDK1.7开始追加有AutoCloseable接口，实际上这个借口的主要目的是希望可以进行自动关闭的处理，不过这种处理一般不好用，需要特殊的语法结构完成。如果想要实现这种处理，那么必须结合try-catch

**范例** 观察AutoCloseable接口：

class Message implements AutoCloseable{
	public  Message() {
		System.out.println("创建一条新的消息！");
	}
	public void print() {
		System.out.println("www.mldn.cn");
	}
	@Override
	public void close() throws Exception {//关闭处理操作
		System.out.println("【AutoCloseable接口】进行关闭方法的处理！");
		throw new Exception("就不关！");
	}
}
public class TestAutoDemo {
	public static void main(String[] args)throws Exception {
		try(Message msg = new Message()){//必须在try语句中定义对象
			msg.print();
		}catch (Exception e) {
			e.printStackTrace();
		}
	}

}

**console：**

	创建一条新的消息！
	www.mldn.cn
	【AutoCloseable接口】进行关闭方法的处理！
	java.lang.Exception: 就不关！
	at cn.mldn.demo.Message.close(TestAutoDemo.java:13)
	at cn.mldn.demo.TestAutoDemo.main(TestAutoDemo.java:20)
这种自动的关闭处理需要针对try语句进行变更，从语法结构上不太习惯。

**范例** 使用自动关闭之前的操作：

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
			try(OutputStream output = new FileOutputStream(file,true)){//意味着只能够进行文件处理
				// 3、进行文件的输出操作
				String msg = "www.mldn.cn\r\n";// 这个是要求输出的内容
				output.write(msg.getBytes(),0,3);// 将内容变为字节数组
			}catch (Exception e) {
				e.printStackTrace();
			}
		}	
	}

容易产生混乱，了解即可；



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course75)
