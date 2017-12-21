## [上一页](course79)

## 包装类（字符串与基本数据类型转换）

以后要进行各种数据的输入一定都是字符串类型的接收，所以在开发之中存在有一种需求，如何将字符串变为各个基本数据类型，这个时候就需要包装类支持了：

- String变为int类型（Integer类）：
		
		|- public static int parseInt(String s)

- String变为double类型（Double类）：

		|- public static double parseDouble(String s)

- String变为boolean类型（Boolean类）：

		|- public static boolean parseBoolean(String s)

- String变为character类型：
		
		public class TestDemo {
			public static void main(String[] args) {
				String str = "hello";
				for (int j = 0; j < str.length(); j++) {
					System.out.print(str.charAt(j) + ",");
				}
			}
		}

**console：**

	h,e,l,l,o,

**范例** 将字符串变为int型：

	public class TestDemo {
		public static void main(String[] args) {
			String str = "123";//字符串
			int num = Integer.parseInt(str);//字符串变为基本类型
			System.out.println(num * 2);
		}
	}

**console：**

	246

**范例** 将字符串变为double型：

	public class TestDemo {
		public static void main(String[] args) {
			String str = "123";//字符串
			double num = Double.parseDouble(str);//字符串变为基本类型
			System.out.println(num * 2);
		}
	}

**console：**

	246.0

但是特别要引起注意的是，如果在将字符串变为数字的时候，字符串有非数字，那么转换就将出现错误（NumberFormatException），因为这个异常，我们要写一堆的程序来回避。

特别需要说明的是字符串与Boolean转换就不受多少局限了。
	
	public static boolean parseBoolean(String s) {
		 return ((s != null) && s.equalsIgnoreCase("true"));
	}

**范例** 将字符串变为boolean型：

	public class TestDemo {
		public static void main(String[] args) {
			String str = "true";//字符串
			String str1 = "something";
			boolean num = Boolean.parseBoolean(str);//字符串变为基本类型
			boolean num1 = Boolean.parseBoolean(str1);
			System.out.println(num);
			System.out.println(num1);
		}
	}
**console：**

	true
	false

如果在进行boolean处理的时候发现字符串的组成不是true或者false，那么将统一按照false进行处理

那么如果现在想要将基本数据类型变为字符串则有两种形式：

- 任何的数据类型使用了“+”连接空白字符串就变成了字符串；

		public class TestDemo {
			public static void main(String[] args) {
				String str = 100 + "";
				System.out.println(str.length());
			}
		}

		**console：**
		3

- 使用String类中提供的valueOf方法，这个方法可以进行转换，而且被重载了很多次

		public class TestDemo {
			public static void main(String[] args) {
				String str = String.valueOf(100);
				System.out.println(str.length());
			}
		}

		**console：**
		3

这个操作作为基本概念知道即可，以后的开发一定会涉及到字符串转其他基本数据类型的处理。

## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course81)
