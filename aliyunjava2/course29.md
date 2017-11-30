## [上一页](course28)

## 8.5 String类的常用方法（字符串查找）

从一个完整的字符串之中可以判断指定的内容是否存在，对于字符串的查找方法有很多定义

 No.| 方法名称 | 类型 | 描述
 -|---|------|------|
 01| public boolean contains(CharSequence s)  |普通 | 判断一个子字符串是否存在
 02| public int indexOf(String str)  |普通 | 从头开始查找指定字符串的位置，查到了返回指定字符串的开始索引，如果查不到返回-1
 03| public int indexOf(String str,int fromIndex)  |普通 | 从指定位置开始查找字符串的位置
 04| public int lastIndexOf(String str)  |普通 | 从后向前查找子字符串的位置
 05| public int lastIndexOf(String str，int fromIndex)  |普通 | 从后向前查找子字符串的位置，从指定位置开始
 06| public boolean startsWith(String prefix)  |普通 | 判断是否以指定字符串开头
 07| public boolean startsWith(String prefix，int toffset)  |普通 | 从指定位置开始判断是否以指定字符串开头
 08| public boolean endsWith(String suffix)  |普通 | 判断是否以指定字符串结尾

**范例** 字符串查找，最方便的就是contains（），直接返回boolean类型：

	public class StringDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub		
			String str = "helloworld";
			System.out.println(str.contains("world"));
		}
	}

**console：**

	true

该判断形式是从JDK1.5之后开始追加的，在JDK1.5之前需要通过indexOf（）来完成。

**范例** 使用indexOf（）方法进行位置查找1：

	public class StringDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub		
			String str = "helloworld";
			System.out.println(str.indexOf("world"));//5,w开始的索引
			System.out.println(str.indexOf("java"));//-1，没有找到
			if(str.indexOf("world") != -1) {
				System.out.println("指定内容可以查找到！");
			}
		}
	}

**console：**

	5
	-1
	指定内容可以查找到！

但是现在都使用contains（）方法来完成。

但是indexOf（）方法需要注意的是，如果内容重复，它只能够返回查找的第一个位置。

**范例** 使用indexOf（）方法进行位置查找2：

	public class StringDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub		
			String str = "helloworld";
			System.out.println(str.indexOf("l"));//2，第一个l出现的位置
			System.out.println(str.indexOf("l",5));//8,world中的l
			System.out.println(str.lastIndexOf("l"));//8
			System.out.println(str.indexOf("java"));//-1，没有找到
			if(str.indexOf("world") != -1) {
				System.out.println("指定内容可以查找到！");
			}
		}
	}

**console：**
	
	2
	8
	8
	-1
	指定内容可以查找到！

在进行查找的时候往往会判断开头或者结尾。

**范例** 判断开头或者结尾：

	public class StringDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub		
			String str = "**@@helloworld##";
			System.out.println(str.startsWith("**"));
			System.out.println(str.startsWith("@@",2));
			System.out.println(str.endsWith("##"));
		}
	}

**console：**

	true
	true
	true

很多时候往往一些参数会利用一些标记进行特殊处理，此时就需要使用到startWith（）或endWith（）方法。


## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course30)
