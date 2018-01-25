## [上一页](course88)
##  System类对IO的支持（系统输入）

System.in对应的类型是InputStream，而这种输入流指的是由用户通过键盘进行输入（用户输入），Java本身并没有直接的用户输入处理，如果想要实现这种输入处理必须用java.io的模式来处理。

**范例** 利用InputStream实现用户的输入：

	import java.io.InputStream;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			InputStream input = System.in;//为父类实例化
			byte data[] = new byte[1024]; //开辟一个空间
			System.out.println("请输入信息：");
			int temp = input.read(data);//读取字节到字节数组中
			System.out.println("【ECHO】 输入内容为： " + new String(data,0,temp));
		}
	}
**console：**

	请输入信息：
	what's this?
	【ECHO】 输入内容为： what's this?

再输入数据的时候程序需要进行暂停，也就是说程序需要进入阻塞状态。直到用户输入完成（按下回车），才能够继续向下执行。但是以上的程序本身有一个致命的问题，核心在于：要开辟的数组空间长度是固定的，如果现在输入的内容超过了该长度，那么只能够接收部分数据。所以这个时候是由于一次读取不玩所造成的，所以此时最好的做法是引入内存操作流来进行控制，也就是说这些数据暂时保存在内存流里面，而后通过内存流一次性取出。

**范例** 改进输入设计：

	import java.io.ByteArrayOutputStream;
	import java.io.InputStream;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			InputStream input = System.in;//为父类实例化
			ByteArrayOutputStream bos = new ByteArrayOutputStream();
			byte data[] = new byte[10]; //开辟一个空间
			System.out.println("请输入信息：");
			int temp = 0;
			while ((temp = input.read(data)) != -1) {//数据读取到字节数组中
				//这里面需要由用户自己来处理换行的问题，因为换行不属于文件结束，所以输入不是-1
				bos.write(data, 0, temp);//保存在内存输出流
				if (temp < data.length) {
					break;
				}
			}
			System.out.println("【ECHO】 输入内容为： " + new String(bos.toByteArray()));
			bos.close();
			input.close();
		}
	}
**console：**

	请输入信息：
	今天下午没有课，挺风和日丽的
	
	【ECHO】 输入内容为： 今天下午没有课，挺风和日丽的

现在虽然实现了键盘输入数据的功能，不过整体实现逻辑有些过于混乱了，也就是说Java本身提供的System.in该操作不好用。

以上的操作充分考虑到了中文问题，处理起来很麻烦，而如果只考虑英文，代码就可以按照如下方式实现：

	import java.io.InputStream;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			InputStream input = System.in;//为父类实例化
			StringBuffer buf = new StringBuffer();
			System.out.println("请输入信息：");
			int temp = 0;
			while ((temp = input.read()) != -1) {
				buf.append((char)temp);
				if(temp == '\n') {
					break;
				}
			}
			System.out.println("【ECHO】 输入内容为： " + buf);
			input.close();
		}
	}
**console：**

	请输入信息：
	helloworld!
	【ECHO】 输入内容为： helloworld!

	请输入信息：
	今天天气很差
	【ECHO】 输入内容为： ???ì?ì??????

通过以上的比较可以感受到System.in的支持度不高，对于英文的操作还勉强可以使用，而如果是中文的操作就必须结合内存流来完成，所以复杂度很高，如果开发中采用这样的模式，就会非常麻烦。

如果想要在IO中进行中文的处理，那么最好的做法是将所有的输入数据保存在以后再处理，这样才可以保证不出现乱


## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course90)
