## [上一页](course31)

## 8.8 String类的常用方法（字符串截取）

从一个完整的字符串中截取出部分内容，那么对于截取的方法有如下几个：

 No.| 方法名称 | 类型 | 描述
 -|---|------|------|
 01| public String substring(int beginIndex) | 普通 | 从指定索引截取到结尾
 02| public String substring(int beginIndex,int endIndex) |普通 |从指定索引截取部分内容

**范例** 字符串的截取操作：

	public class StringDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub		
			String str = "helloworld";
			System.out.println(str.substring(5));
			System.out.println(str.substring(0,5));
		}
	}

**console：**

	world
	hello

千万记住，程序中字符串的索引从0开始，而且只能够设置正整数，不能使用负数。

## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course33)
