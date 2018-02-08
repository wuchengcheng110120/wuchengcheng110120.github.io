## [上一页](course117)
##  网络编程（Echo模型）

网络编程有一个最为经典的程序案例：Echo程序，所谓的Echo程序的核心本质在于：将用户接收到的数据前面追加一个“Echo”的头信息进行返回。这个程序要求用户可以一直进行信息的输入，一直到用户输入byebye才表示操作结束。

**范例** 编写服务器端：

	package cn.mldn.netdemo.echo;
	
	import java.io.PrintStream;
	import java.net.ServerSocket;
	import java.net.Socket;
	import java.util.Scanner;
	
	public class EchoServer {
		public static void main(String[] args) throws Exception {
			ServerSocket server = new ServerSocket(8888);
			Socket client = server.accept(); // 等待连接
			Scanner scan = new Scanner(client.getInputStream()); // 接收客户端输入
			scan.useDelimiter("\n");
			PrintStream out = new PrintStream(client.getOutputStream()); // 对客户端的回应信息
			boolean flag = true; // 作为循环的处理标记
			while (flag) { // 相当于一直循环
				if (scan.hasNext()) { // 现在客户端有数据发送
					String str = scan.next().trim(); // 防止有多余空格出现
					if ("byebye".equalsIgnoreCase(str)) { // 操作结束
						out.print("byebye!!!");
						flag = false; // 此时循环退出
						break; // 退出循环
					}
					out.println("Echo : " + str); // 做出回应
				}
			}
			out.close();
			scan.close();
			server.close();
		}
	}

随后编写客户端，客户端肯定要用户自己来输入数据，自己来输入数据就需要使用System.in,并且结合Scanner进行操作

**范例** 客户端实现：

	package cn.mldn.netdemo.echo;
	
	import java.io.PrintStream;
	import java.net.Socket;
	import java.util.Scanner;
	
	public class EchoClient {
		public static void main(String[] args) throws Exception {
			Socket client = new Socket("localhost", 8888);
			Scanner keyScan = new Scanner(System.in);
			keyScan.useDelimiter("\n");
			Scanner netScan = new Scanner(client.getInputStream());
			netScan.useDelimiter("\n");
			PrintStream netOut = new PrintStream(client.getOutputStream());
			boolean flag = true;
			String str = null;
			while (flag) {
				System.out.println("请输入要发送的信息：");
				if (keyScan.hasNext()) {
					str = keyScan.next().trim();
					netOut.println(str);  // 发送给服务器端
					if (netScan.hasNext()) { // 服务器端有回应
						System.out.println(netScan.next());
					}
				}
				if ("byebye".equalsIgnoreCase(str)) {
					flag = false;
					break;
				}	
			}
			keyScan.close();
			netScan.close();
			client.close();
		}
	}


以上完成了一个基础程序，但是程序有一个问题，本程序为单线程，因为所有的操作都是在主方法里进行的。

要想解决当前的问题就必须进行多线程的处理，把每一个连接的用户都封装在一个线程里面，这样处理起来就可以不受到单线程的局限了。

	package cn.mldn.netdemo.echo;
	
	import java.io.PrintStream;
	import java.net.ServerSocket;
	import java.net.Socket;
	import java.util.Scanner;
	
	public class EchoServer {
		public static void main(String[] args) throws Exception {
			ServerSocket server = new ServerSocket(8888);
			boolean flag = true;
			while (flag) {
				Socket client = server.accept(); // 等待连接
				new Thread(new MyThread(client)).start();
			}
			server.close();
		}
		public static class MyThread implements Runnable{
			private Socket client ;
			public  MyThread(Socket client) {
				this.client = client;
			}
			@Override
			public void run() {
				try {
					Scanner scan = new Scanner(client.getInputStream()); // 接收客户端输入
					scan.useDelimiter("\n");
					PrintStream out = new PrintStream(client.getOutputStream()); // 对客户端的回应信息
					boolean flag = true; // 作为循环的处理标记
					while (flag) { // 相当于一直循环
						if (scan.hasNext()) { // 现在客户端有数据发送
							String str = scan.next().trim(); // 防止有多余空格出现
							if ("byebye".equalsIgnoreCase(str)) { // 操作结束
								out.print("byebye!!!");
								flag = false; // 此时循环退出
								break; // 退出循环
							}
							out.println("Echo : " + str); // 做出回应
						}
					}
					out.close();
					scan.close();
					
				} catch (Exception e) {
					e.printStackTrace();
				}
			}
		}
	}

实际上所有的服务器上，每一个用户的连接对于服务器都是一个线程，而所谓的线程同步指的就是对共享资源的控制。

网络编程的时代结束了，现在不再进行这样的网络编程。

多线程 + IO + 输入输出   ：可以写服务器代码了。


## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course119)
