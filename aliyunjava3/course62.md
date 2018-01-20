## [上一页](course61)
## Base64加密处理

JDK1.8才有，Base64是一种数据加密算法，利用这个算法可以实现信息的安全处理。

如果想要进行加密处理可以使用两个：加密器、解密器。

**范例** 观察这种加密处理：

	package cn.mldn.demo;
	
	import java.util.Base64;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			String msg = "www.mldn.cn";//源文件
			String eMsg = Base64.getEncoder().encodeToString(msg.getBytes());//加密处理需要用比特数组完成
			System.out.println("加密后的信息: " + eMsg);
			byte [] dMsg = Base64.getDecoder().decode(eMsg);
			System.out.println("解密后的信息: " + new String(dMsg));
			
		}
	}
**console：**

	加密后的信息: d3d3Lm1sZG4uY24=
	解密后的信息: www.mldn.cn

具体的原理与密码学相关。

如果只使用Base64加密和没加密一样，因为输入相同数据加密算法产生结果相同。

一般采用多次加密。

	package cn.mldn.demo;
	
	import java.util.Base64;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			String msg = "www.mldn.cn";//源文件
			String eMsg = encode(encode(encode(msg)));//加密处理需要用比特数组完成
			System.out.println("加密后的信息: " + eMsg);
		}
		public static String encode(String msg) {
			return Base64.getEncoder().encodeToString(msg.getBytes());
		}
	}
**console：**

	加密后的信息: WkROa00weHRNWE5hUnpSMVdUSTBQUT09

还有一种做法就是种子数：

	package cn.mldn.demo;
	
	import java.util.Base64;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			String seed = encode("mldnjava-hahah");//密钥
			String msg = "www.mldn.cn" + "("+seed+")";//源文件 + 密钥
			String eMsg = encode(encode(encode(msg)));//加密处理需要用比特数组完成
			System.out.println("加密后的信息: " + eMsg);
		}
		public static String encode(String msg) {
			return Base64.getEncoder().encodeToString(msg.getBytes());
		}
	}
**console：**

	加密后的信息: WkROa00weHRNWE5hUnpSMVdUSTBiMWxzWkRSaE1rcDBZMGRvYTJKVlZqQlpWV1JIWWpGc1dGcDZNSEE9


以后的开发中将Base64和MD5加密一起完，长度变为32位。



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course63)
