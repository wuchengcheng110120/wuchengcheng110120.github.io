## [上一页](course66)
## 【第09个代码模型】正则表达式（java.util.regex开发包）

从JDK1.4开始增加的开发包java.util.regex，但是在这个包里面只有两个类：Pattern类、Matcher类。Pattern负责编译正则，而Matcher负责匹配正则。如果做得是一般的处理实际上不需要使用这两个类，只需要使用String即可。

1、 观察Pattern中的方法：

- 取得实例化对象：public static Pattern compile(String regex)；

- 拆分字符串：public String[] split(CharSequence input)；

- 取得matcher类对象：public Matcher matcher(CharSequence input)

**范例** 通过Pattern类进行字符串拆分：

	import java.util.regex.Pattern;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			String str  = "a|b|c";
			String regex = "\\|";
			Pattern pat = Pattern.compile(regex);
			String result[] = pat.split(str);
			for (int i = 0; i < result.length; i++) {
				System.out.print(result[i]);
			}
		}
	}
**console：**

	abc

2、 Matcher负责进行正则匹配：

- 字符串匹配; public boolean matches();

- 全部替换：public String replaceAll(String replacement)；

- 替换首个： public String replaceFirst(String replacement)；

**范例** 匹配：

	import java.util.regex.Matcher;
	import java.util.regex.Pattern;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			String str  = "100";
			String regex = "\\d+";
			Pattern pat = Pattern.compile(regex);
			Matcher mat = pat.matcher(str);
			System.out.println(mat.matches());
		}
	}
**console：**

	true
在进行复杂的正则操作时，String类是完成不了的，必须通过Matcher类进行处理，因为其中有分组的概念。

	import java.util.regex.Matcher;
	import java.util.regex.Pattern;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			String str  = "INSERT INTO member(mid,name,age) VALUES (#{member.mid},#{member.name},#{member.age})";
			String regex = "#\\{[a-zA-Z_0-9\\.]+\\}";//分组的依据
			Pattern pat = Pattern.compile(regex);
			Matcher mat = pat.matcher(str);
			while(mat.find()) {
				System.out.println(mat.group(0));
			}
		}
	}
**console：**

	#{member.mid}
	#{member.name}
	#{member.age}

基本上开发中最常使用的正则都在String中有所定义了，而如果一些复杂的操作才会使用Matcher类或者Pattern类来执行，这种情况比较少见；

重点：

1、 正则标记；

2、 String类对正则的支持；

## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course68)
