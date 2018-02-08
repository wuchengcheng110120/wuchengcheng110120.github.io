## [上一页](course116)
##  网络编程（基本网络程序模型）

下面准备编写一个服务器端的代码和一个客户端代码，主要是通过客户端连接服务器端取得一些信息，服务器端只输出一次“Hello World !” 就表示操作结束。

如果要开发网络程序使用java.net程序包即可，这个包内有两个类：ServerSocket（服务器）、Socket（客户端）。

**范例** 编写一个服务器端程序：

	package cn.mldn.netdemo.server.hello.server;
	
	import java.io.PrintWriter;
	import java.net.ServerSocket;
	import java.net.Socket;
	
	public class HelloServer {
		public static void main(String[] args) throws Exception{
			//1、创建一个服务器端的服务对象,所有的服务一定要有一个监听端口
			ServerSocket server = new ServerSocket(9999); //此时的服务在9999端口等待连接
			System.out.println("等待客户来连接......");
			//2、需要等待客户连接，也就是说此时的程序在此处会进入到一个阻塞状态
			Socket client = server.accept(); // 表示等待连接，连接的都是客户
			PrintWriter out = new PrintWriter(client.getOutputStream());
			out.println("Hello World !"); // 要有换行
			out.close();
			server.close();
		}
	}

**范例** 编写一个客户端程序：

	package cn.mldn.netdemo.server.hello.client;
	
	import java.net.Socket;
	import java.util.Scanner;
	
	public class HelloClient {
		public static void main(String[] args) throws Exception{
			//1、 表示连接到指定的服务器端的主机名称和端口，localhost =127.0.0.1
			Socket client = new Socket("localhost", 9999);
			//2、 等待进行服务器的输出，服务器的输出对客户是输入
			Scanner scan = new Scanner(client.getInputStream());
			scan.useDelimiter("\n");
			if (scan.hasNext()) {
				System.out.println(scan.next());
			}
			client.close();
		}
	}
这个时候的服务器实际上只能够处理一次请求




## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course118)
