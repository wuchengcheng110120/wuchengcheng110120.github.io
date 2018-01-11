## [上一页](course46)
## 【第07个代码模型】 日期处理类（SimpleDateFormat类）

日期格式化；

使用Date取得的日期时间的数据实际上结构并不好，或者说这样的结构不符合日期阅读习惯，需要对日期进行格式化处理。

使用的是java.text包中的内容。


java.lang.Object

java.text.Format
	
	public final String format(Object obj)

java.text.DateFormat    

	public final String format(Date date)

	public Date parse(String source)throws ParseException

java.text.SimpleDateFormat   

	public SimpleDateFormat(String pattern)


![](http://ww4.sinaimg.cn/large/0060lm7Tly1fncnnsqlh4j30vh0he7bo.jpg)

日期格式化里面需要设计一些日期标记：年(yyyy)、月(MM)、日(dd)、时(HH)、分(mm)、秒(ss)、毫秒(SSS)

**范例** 实现日期的格式化处理（日期格式化之后就是字符串）

	package cn.mldn.demo;
	import java.text.SimpleDateFormat;
	import java.util.Date;
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			String str =  "yyyy-MM-dd HH:mm:ss.SSS";
			Date date = new Date();//当前的日期时间
			SimpleDateFormat sdf = new SimpleDateFormat(str);//定义转换类，同时设置模板
			String val = sdf.format(date);//将日期进行格式化处理
			System.out.println(val);
		}
	}
**console：**

	2018-01-11 14:51:28.457

**范例** 将字符串变为Date类型

package cn.mldn.demo;
import java.text.SimpleDateFormat;
import java.util.Date;
public class TestDemo {
	public static void main(String[] args) throws Exception {
		String str = "1911-11-11 11:11:11.111";
		String pat =  "yyyy-MM-dd HH:mm:ss.SSS";
		SimpleDateFormat sdf = new SimpleDateFormat(pat);//定义转换类，同时设置模板
		Date date = sdf.parse(str);//当前的日期时间
		System.out.println(date);
	}
}

**console：**

	Sat Nov 11 11:11:11 CST 1911

这种格式在开发中会经常使用



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course48)
