## [上一页](course21)

## 7.3 String类的基本特点（字符串为匿名对象）

字符串常量是String的匿名对象；

任何语言的底层都不可能会提供有直接的字符串类型。现在所谓的字符串只是高级语言提供给用户方便开发的支持而已。所以在java里面本身也没有直接提供有字符串常量的概念，所有使用“""”定义的内容本质上来讲都是String的匿名对象。

**范例** 观察字符串操作：

	public class StringDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			String str = "hello";
			System.out.println(str.equals("hello"));
			System.out.println("hello".equals(str));
		}
	}

**console：**

	true
	true

之前出现的“String str = "hello"”,本质上就是讲一个匿名的String类对象设置有名字，而且匿名对象一定保存在堆内存之中。

**提醒**：在开发过程中，如果要判断用户输入的字符串是否等同于指定的字符串，一定要将字符串写在前面。

- 比较的操作方法1：

**范例** 用户没有数据输入：

	public class StringDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			String input = null;//假设由用户输入
			System.out.println(input.equals("hello"));
		}
	}

**console：**

	Exception in thread "main" java.lang.NullPointerException
		at bznoc171118.StringDemo.main(StringDemo.java:7)

在进行数据接受的时候必须要考虑用户没有输入数据的问题，如果说以上面的代码为例，用户没有输入则执行的时候一定会出现“NullPointerException”问题。

- 任何的字符串常量都是String匿名对象，所以该对象不能为null

**范例** 用户没有数据输入：

	public class StringDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			String input = null;//假设由用户输入
			System.out.println("hello".equals(input));
		}
	}

**console：**

	false

以后在进行比较的时候建议采用如上的写法，把字符串写在前面，即字符串作为匿名对象调用equals（）方法与输入进行比较。

## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course23)
