## [上一页](course65)
## 【第09个代码模型】正则表达式（String类对正则的支持）

从JDK1.4开始String类发生了一些改变，也就是说用户可以直接通过String类来进行正则的调用，在String类里面有如下几个直接支持正则开发的方法：

-  public boolean matches(String regex)，普通方法，进行字符串验证的，匹配某个正则；

-  public String replaceAll(String regex,
                         String replacement)，普通方法，根据正则的描述替换全部；

- public String replaceFirst(String regex,
                           String replacement)，普通方法，根据正则替换首个；

- public String[] split(String regex)，普通方法，根据正则进行拆分；

- public String[] split(String regex,
                      int limit)， 普通方法，根据正则拆分成制定个数；


**范例** 实现字符串替换：

	package cn.mldn.demo;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			String str = "sfasfdsdf*//*sdfasf64r563@#$@#$";
			String regex = "[^a-zA-Z]";//正则
			System.out.println(str.replaceAll(regex, ""));//把所有非字母换成空
		}
	}
**console：**

	sfasfdsdfsdfasfr


**范例** 实现字符串拆分：

	package cn.mldn.demo;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			String str = "a11b222c3dd4444444e555f";
			String regex = "\\d+";//正则
			String result[] = str.split(regex) ;
			for (int i = 0; i < result.length; i++) {
				System.out.print(result[i]);
			}
		}
	}

**console：**

	abcddef

在使用正则过程中最为麻烦的部分就是进行字符串验证

**范例**验证某一字符串是否是数字（整数或者小数），如果是则将其变为Double型：

	package cn.mldn.demo;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			String str = "11010";
			String regex = "\\d+(\\.\\d+)?";//正则
			if (str.matches(regex)) {//匹配成功
				double data = Double.parseDouble(str);
				System.out.println(data);
			}
		}
	}
**console：**

	11010.0

**范例**验证某一字符串是否是日期或者日期时间，如果是则将其变为Date类型：

	package cn.mldn.demo;
	
	import java.text.SimpleDateFormat;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			String str = "2018-10-12 10:11:12";
			String regex = "\\d{4}-\\d{2}-\\d{2}";//正则
			if (str.matches(regex)) {//匹配成功
				System.out.println(new SimpleDateFormat("yyyy-MM-dd").parse(str));
			}else if (str.matches("\\d{4}-\\d{2}-\\d{2} \\d{2}:\\d{2}:\\d{2}")) {
				System.out.println(new SimpleDateFormat("yyyy-MM-dd hh:mm:ss").parse(str));
			}
		}
	}
**console：**

	Fri Oct 12 10:11:12 CST 2018	

此时这种需要转换的前提下，正则的格式判断最好分开编写。

**范例**判断给定的电话号码是否正确（用一个正则进行判断）：

- 电话格式一： 51283346【\\d{7,8}】；

- 电话格式二： 01051283346【(\\d{3-4})?\\d{7,8}】；

- 电话格式三： （010）- 51283346【((\\(\\d{3-4}\\)-)|(\\d{3-4}))?\\d{7,8}】；

	package cn.mldn.demo;
	
	import java.text.SimpleDateFormat;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			String str = "(010)-51283346";
			String regex = "((\\(\\d{3,4}\\)-)|(\\d{3,4}))?\\d{7,8}";//正则
			System.out.println(str.matches(regex));
		}
	}

**console**

	true

**范例**验证给定的字符串是否是email地址：

- 简单验证：邮件地址由字母、数字、“_”所组成；

	public class TestDemo {
		public static void main(String[] args) throws Exception {
			String str = "a@a.a";
			String regex = "\\w+@\\w+\\.\\w+";//正则
			System.out.println(str.matches(regex));
		}
	}

- email的用户名必须由字母开头，而且组成可以是字母、数字、“_”、“-”、“.”所组成，而且用户名长度必须在6到15位之间，且用户名的后缀必须是.com、.net、.cn、.org、.gov、.com.cn、.net.cn。

![](https://s1.ax1x.com/2018/01/21/pWvHOA.png)

	public class TestDemo {
		public static void main(String[] args) throws Exception {
			String str = "amldn88-1.2@mldnjava.cn";
			String regex = "[a-zA-Z][a-zA-Z\\._\\-0-9]{5,14}@[a-zA-Z\\\\._\\-0-9]+\\.(com|net|cn|org|gov|edu|com\\.cn|net\\.cn)";//正则
			System.out.println(str.matches(regex));
		}
	}

**console：**

	true


## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course67)
