## [上一页](course26)

## 8.3 String类的常用方法（字节与字符串）

字节更多的情况是用于数据传输及编码转换处理之中，在String类中提供有字节处理的支持。


 No.| 方法名称 | 类型 | 描述
 -|---|------|------|
 01| public String(byte[] bytes)  | 构造  | 将字节数组转换为字符串
 02| public String(byte[] bytes,int offset，int length)  |  构造 |将部分字节数组转换为字符串 
 03| public byte[] getBytes()  | 普通 | 将字符串以字节数组的形式返回
 04| public byte[] getBytes(String charsetName)throws UnsupportedEncodingException| 普通 | 将字符串进行编码转换，转码处理

**范例** 实现字符串与字节数组的转换处理：

	public class StringDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub		
			String str = "helloworld";//String str = "世界和平";
			byte data[] = str.getBytes();
			for(int x = 0; x < data.length ; x++) {
				data[x] -= 32;
				System.out.print(data[x]+ "、");
				
			}
			System.out.print(new String(data));
		}
	}

**console：**

	72、69、76、76、79、87、79、82、76、68、HELLOWORLD

通过尝试发现，字节并不适合处理中文，而只有字符适合处理中文，并且按照程序的概念来讲，1个字符等于2个字节，字节只适合于处理二进制数据。

## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course28)
