## [上一页](course60)
## UUID类

UUID类是根据当前的地址还有时间戳自动生成一个几乎不会重复的字符串，在以后的实际项目开发过程中经常需要使用一些上传处理操作，这个时候就需要使用到UUID这个类了。

在进行简单开发的时候可以使用UUID类生成一些简单的文件名称。以防止重名问题的出现。

	package cn.mldn.demo;
	
	import java.util.UUID;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			UUID uuid = UUID.randomUUID();//根据当前地址和时间戳取得一个内容
			System.out.println(uuid.toString());
		}
	}

**console：**

	5f079934-7869-4815-a806-44d73efced12
	


## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course62)
