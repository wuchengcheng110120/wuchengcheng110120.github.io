## [上一页](course89)
##  BufferedReader类

BufferedReader类属于一个缓冲的输入流，而且是一个字符流的操作对象。但是必须要清楚一点，对于缓冲流在java.io中定义有两类：字节缓冲流（BufferedInputStream）、字符缓冲流（BufferedReader）。

之所以选择字符缓冲流（BufferedReader）操作是因为在此类中提供的readLine()方法，这个方法可以读取一行数据（以回车为换行符）：

	|- 读取一行： public String readLine()
                throws IOException
但是如果要想使用BufferedReader类有一个问题需要注意，来观察BufferedReader类的定义以及构造方法：

	|-java.lang.Object
		|-java.io.Reader
			|-java.io.BufferedReader

	public class BufferedReader
	extends Reader

	构造方法：public BufferedReader(Reader in)

![](http://ww3.sinaimg.cn/large/0060lm7Tly1fnt0hyp4xzj30vc0hc7a8.jpg)

**范例** 利用BufferedReader类实现键盘输入：

import java.io.BufferedReader;
import java.io.InputStreamReader;

public class TestDemo {
	public static void main(String[] args) throws Exception {
		BufferedReader buf = new BufferedReader(new InputStreamReader(System.in));
		System.out.print("请输入信息：");
		//默认的换行模式是BufferedReader的一个最大缺点，如果不是因为此缺点该类还会继续使用
		String str = buf.readLine(); //接收输入信息，默认使用回车换行
		System.out.println("【ECHO】输入信息为：" + str);
	}
}
**console：**

	请输入信息：今天很好
	【ECHO】输入信息为：今天很好
使用以上的键盘输入还有一个最大的特点，由于接收数据类型为str，那么证明可以使用正则判断，可以利用String类的各种操作进行数据处理，还可以变为各种常用的数据类型。

**范例** 由键盘输入数字，不是数字则报错：

	import java.io.BufferedReader;
	import java.io.InputStreamReader;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			BufferedReader buf = new BufferedReader(new InputStreamReader(System.in));
			System.out.print("请输入信息：");
			//默认的换行模式是BufferedReader的一个最大缺点，如果不是因为此缺点该类还会继续使用
			String str = buf.readLine(); //接收输入信息，默认使用回车换行
			if (str.matches("\\d{1,3}")) {//是一个数数字
				System.out.println("【ECHO】输入信息为：" + Integer.parseInt(str));
			}else {
				System.out.println("输入数据有错误！");
			}
		}
	}
**console：**

	请输入信息：1234
	输入数据有错误！

	请输入信息：123
	【ECHO】输入信息为：123

在很多开发中可能还可以看到BufferedReader类的身影，但是这个类随着时间的推移使用频率已经很低了，已经被新的类Scanner取代了。


## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course91)
