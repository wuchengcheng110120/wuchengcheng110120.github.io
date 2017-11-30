## [上一页](course30)

## 8.7 String类的常用方法（字符串拆分）

在整个字符串中，可以使用一个特定的字符串来实现字符串分割处理，也就是说可以将一个完整的字符串，按照指定的分隔符划分为若干个子字符串。

 No.| 方法名称 | 类型 | 描述
 -|---|------|------|
 01| public String[] split(String regex)  | 普通 | 将字符串全部拆分
 02| public String[] split(String regex,int limit) |普通 |将字符串部分拆分，该字符串数组长度就是limit的极限

**范例** 实现字符串拆分处理：

	public class StringDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub		
			String str = "hello world hello mldn";
			String result [] = str.split(" ");
			for(int x=0; x <result.length ; x++) {
				System.out.println(result[x]);			
			}
		}
	}

**console：**

	hello
	world
	hello
	mldn

**范例** 实现字符串部分拆分处理：

	public class StringDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub		
			String str = "hello world hello mldn";
			String result [] = str.split(" ",2);
			for(int x=0; x <result.length ; x++) {
				System.out.println(result[x]);			
			}
		}
	}

**console：**

	hello
	world hello mldn

以上的拆分形式都很容易，如果发现有些内容无法拆分开，就需要使用“\\”进行转义。

**范例** 拆分IP地址：

	public class StringDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub		
			String str = "192.168.1.1";
			String result [] = str.split("\\.");
			for(int x=0; x <result.length ; x++) {
				System.out.println(result[x]);			
			}
		}
	}

**console：**

	192
	168
	1
	1

在以后的实际开发之中，经常会出现这样的拆分模式：姓名：年龄|姓名：年龄|...

**范例** 多次拆分：

	public class StringDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub		
			String str = "SMITH:10|ALLEN:20";
			String result [] = str.split("\\|");
			for(int x=0; x <result.length ; x++) {
				String temp[] = result[x].split("\\:");
				System.out.println(temp[0] + " = " + temp[1]);			
			}
		}
	}

**console：**

	SMITH = 10
	ALLEN = 20

这样的代码在以后的开发之中会经常出现。


## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course32)
