## [上一页](course32)
## 8.9 String类的常用方法（字符串其他操作方法）

在String类中还定义有一些比较小的操作方法。

 No.| 方法名称 | 类型 | 描述
 -|---|------|------|
 01| public String trim() | 普通 | 去掉字符串中的左右空格
 02| public String toUpperCase() |普通 | 字符串转大写
 03| public String toLowerCase() |普通 | 字符串转小写
 04| public String intern() |普通 | 字符串进入对象池
 05| public String concat(String str) |普通 | 字符串连接，等同于“+”
 06| public int length() | 普通 | 取得字符串的长度
 07| public boolean isEmpty() | 普通 | 判断是否为空字符串（但是不是为null，而是为0）

**范例** 观察trim（）方法的使用：

	public class StringDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub		
			String str = "     hello world  ";
			System.out.println(" 【 " + str + "】 ");
			System.out.println(" 【 " + str.trim() + "】 ");
		}
	}

**console：**

	【      hello world  】 
	 【 hello world】 

**范例** 大小写转换：

	public class StringDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub		
			String str = "     hello &*(&*&^*&^*world  ";
			System.out.println(str.toUpperCase() );
			System.out.println(str.toLowerCase() );
		}
	}

**console：**

     HELLO &*(&*&^*&^*WORLD  
     hello &*(&*&^*&^*world 

使用这两个函数不对不是大小写字母的内容进行大小写转换，实际上就少了用户的判断。


**范例** 观察concat（）方法：

	public class StringDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub		
			String str1 = "helloworld";
			String str2 = "hello".concat("world");
			System.out.println(str1 == str2 );
			System.out.println(str1 == str2.intern() );
			System.out.println(str2 );
		}
	}

**console：**

	false
	true
	helloworld

**范例** 取得字符串长度：

	public class StringDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub		
			String str = "helloworld";
			System.out.println(str.length());
		}
	}

**console：**

	10

在数组使用上有一个格式“数组名称.length属性”，但是在String类中length是一个方法，必须通过对象才能调用，而且方法后面一定有“（）”存在。

**范例** 观察isEmpty（）方法：

	public class StringDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub		
			System.out.println("hello".isEmpty());
			System.out.println("".isEmpty());
			System.out.println(new String().isEmpty());
		}
	}

**console：**

	false
	true
	true

在String类中唯一的遗憾是没有提供首字母大写方法，所以如果我们想要使用就必须自己来实现。

**范例** 实现首字母大写：

	public class StringDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub		
			String name = "smith";
			
			System.out.println(initCap(name));
			System.out.println(initCap(""));
			System.out.println(initCap("a"));
		}
		
		public static String initCap(String str) {
			//"".equals(str)和str.isEmpty()
			if (str == null || "".equals(str)) {//没有数据
				return str;
			}
			
			if (str.length() >1) {
				return str.substring(0, 1).toUpperCase() + str.substring(1, str.length());
			}
			
			return str.toUpperCase();
		}
	}

**console：**

	Smith
	
	A

在实际开发中首字母大写的使用频率很高。


## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course34)
