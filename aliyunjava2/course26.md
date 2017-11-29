## [上一页](course25)

## 8.2 String类的常用方法（字符串与字符数组）

字符串就是一个字符数组，String类里面支持字符数组转换为字符串以及字符串变为字符的操作方法。

操作方法定义如下：

 No.| 方法名称 | 类型 | 描述
 -|---|------|------|
 01|  public String(char[] value)  | 构造  | 将字符数组中的所有内容变为字符串
 02|  public String(char[] value,int offset,int count)  | 构造  | 将字符数组中的部分内容变为字符串
 03|  public char charAt(int index)  | 普通  | 取得指定索引位置的一个字符，索引从0开始 
 04|   public char[] toCharArray() | 普通  | 将字符串转换成字符数组返回
 05|   public String toLowerCase() | 普通  | 将字符串中大写字母转换成小写返回

**范例** 观察charAt（）方法：

	public class StringDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub		
			String str = "hello ";
			System.out.println(str.charAt(0));//h
			System.out.println(str.charAt(10));//java.lang.StringIndexOutOfBoundsException
		}
	}

**console：**

	h
	Exception in thread "main" java.lang.StringIndexOutOfBoundsException: String index out of range: 10
		at java.lang.String.charAt(Unknown Source)
		at bznoc171118.StringDemo.main(StringDemo.java:8)

字符串和字符数组的相互转换才是重点。

**范例** 字符串和字符数组的转换：

	public class StringDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub		
			String str = "helloworld";
			char data [] = str.toCharArray();
			for (int x= 0; x<data.length; x++) {
				data[x] -= 32;
				//data[x] = (char)(data[x]-32); 
				System.out.print(data[x] + "、");
			}
			System.out.println();
			//经过处理后所有字符数组都是大写了
			System.out.println(new String(data));
			System.out.println(new String(data,5,5));
		}
	}

**console：**

	H、E、L、L、O、W、O、R、L、D、
	HELLOWORLD
	WORLD

**范例** 现在有一字符串要求判断其是否由数字组成：

- 因为不知道字符串的长度及内容，所以最好的做法是将字符串变为字符数组

- 而后判断每一位字符是否是“‘0’ ~‘9’”之间的内容

		public class StringDemo {
			public static void main(String[] args) {
				// TODO Auto-generated method stub		
				String str = "123l4654";
				System.out.println(isNumber(str)? "全部由数字组成":"含有非数字字符！");	
			}

			//一般而言如果方法返回的是boolean类型，往往以isXxx（）命名
			public static boolean isNumber(String str) {
				char [] data = str.toCharArray();
				for(int x =0; x< str.length(); x++) {
					if(data[x]< '0' || data[x] >'9') {//不是数字
						return false;//后面不需要再继续排查
					}
				}
				return true;//如果都没有错误返回true
			}
		}

**console：**

	含有非数字字符！

很多时候这种根据每一位进行判断的情况会有，但是如果都按照以上的方式操作会很麻烦


## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course27)
