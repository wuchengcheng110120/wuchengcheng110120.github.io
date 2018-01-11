## [上一页](course45)
## 【第07个代码模型】 日期处理类（Date类）

所有的开发必定要有日期；

java.util.Date类是在整个的程序处理之中唯一可以当前日期实例化对象的操作方法，也就是说如果想取得当前日期，直接输出Date类对象即可。

java.lang.Object

java.util.Date

public class Date
extends Object
implements Serializable, Cloneable, Comparable<Date>

	package cn.mldn.demo;
	import java.util.Date;
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			Date date = new Date();
			System.out.println(date);
		}
	}
**console：**

	Thu Jan 11 11:39:28 CST 2018

在Date类中需要关心一个问题：long可以描述日期；

![](http://ww2.sinaimg.cn/large/0060lm7Tly1fncir025blj30by0bvmxp.jpg)

1、 public Date(long date) 构造方法 将long变为Date数据

2、 public long getTime() 普通方法 将Date转为long类型

**范例** 观察转换

	package cn.mldn.demo;
	import java.util.Date;
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			long num = System.currentTimeMillis();//取得当前日期时间数字
			long test = 16561321646L;
			System.out.println(new Date(num));
			System.out.println(new Date(test));
			System.out.println(new Date().getTime());
		}
	}

这种简单的转换，在程序开发中会经常使用；



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course47)
