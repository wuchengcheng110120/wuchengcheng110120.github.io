## [上一页](course29)

## 8.6 String类的常用方法（字符串替换）

使用一个新的字符串替换掉已有字符串的数据，字符串的替换可以使用的方法如下


 No.| 方法名称 | 类型 | 描述
 -|---|------|------|
 01| public String replaceAll(String regex,String replacement)  | 普通 | 替换所有的字符串
 02| public String replaceFirst(String regex,String replacement)  |普通 |替换首个内容

**范例** 实现字符串替换处理：

	public class StringDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub		
			String str = "helloworld";
			System.out.println(str.replaceAll("l", "_"));
			System.out.println(str.replaceFirst("l", "_"));
		}
	}

**console：**

	he__owor_d
	he_loworld

字符串的替换操作与正则表达式有关，后期会详细说明。

## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course31)
