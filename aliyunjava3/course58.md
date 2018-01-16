## [上一页](course57)
## 国际化程序（国际化程序实现）

国际化程序实现的关键就在于不同的资源文件的信息。例如：在当前文件中读取的资源文件名称为：cn.mldn.msg.Message，那么要想定义不同语言的信息，就可以在后面加上语言地区的编码；

**范例** 定义cn.mldn.msg.Message_zh_CN.properties：

 welcome.info = 您好，欢迎您！

**范例** 定义cn.mldn.msg.Message_en_US.properties：

welcome.info = Hello go

**范例** 通过Locale来设置语言和地区信息：

	package cn.mldn.demo;
	
	import java.util.Locale;
	import java.util.ResourceBundle;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			Locale loc = new Locale("en", "US");
			//这个时候设置的baseName没有后缀，而且一定要在CLASSPATH之中
			ResourceBundle res = ResourceBundle.getBundle("cn.mldn.msg.Message",loc);
			System.out.println(res.getString("welcome.info"));
		}
	}

**console：**

	Hello go

如果给出了具体的语言的资源信息，那么原来的Message.properties就没有任何用处了

但是只根据以上内容是不够的，例如，如果输出：您好， xxx！

这个时候就要进行文本格式化的处理。


**范例** 修改资源文件：

	welcome.info = Hello {0}, {1}, {2} go
	
	welcome.info = 您好，{0}, {1}, {2}欢迎您！
	
	package cn.mldn.demo;
	
	import java.text.MessageFormat;
	import java.util.Locale;
	import java.util.ResourceBundle;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			Locale loc =  Locale.getDefault();
			//这个时候设置的baseName没有后缀，而且一定要在CLASSPATH之中
			ResourceBundle res = ResourceBundle.getBundle("cn.mldn.msg.Message",loc);
			String content =res.getString("welcome.info");
			System.out.println(MessageFormat.format(content, "张三","李四","啊天"));
		}
	}

**console：**

	您好，张三, 李四, 啊天欢迎您！

实现的关键就是资源文件的编写。在以后的开发之中会将一些提示的信息放在资源文件里面完成，这种国际化和资源文件的读取处理，一定要掌握。




## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course59)
