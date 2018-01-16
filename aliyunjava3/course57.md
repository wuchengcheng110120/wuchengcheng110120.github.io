
## [上一页](course56)
## 国际化程序（RecourseBundle）

如果要使用资源文件可以使用“java.util.ResourceBundle”类完成，这个类


public abstract class ResourceBundle
extends Object

是一个抽象类，在这个类中提供有一个static方法：public static final ResourceBundle getBundle(String baseName)

这里面所需要的“baseName”实际上就是资源文件的名称（不带*.properties）

**范例** 定义一个资源文件———— cn.mldn.msg.Message.properties，以后资源文件的命名与类名称尽量一致

- 这个文件必须定义在CLASSPATH之中，如果放在包里面则需要加上包名称。该文件采用"key = value" 的形式出现

该文件不允许直接保存中文，所以如果有中文则可以进行转码：JDK\bin\native2ascii.exe，但是这种做法非常麻烦，所以推荐安装一个属性文件编辑器插件：pro	http://propedit.sourceforge.jp/eclipse/updates/	

 	welcome.info = 北京欢迎你

**范例** 使用ResourceBundle类来进行资源读取：

	package cn.mldn.demo;
	
	import java.util.ResourceBundle;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			//这个时候设置的baseName没有后缀，而且一定要在CLASSPATH之中
			ResourceBundle res = ResourceBundle.getBundle("cn.mldn.msg.Message");
			System.out.println(res.getString("welcome.info"));
		}
	}

**console：**

	北京欢迎你

资源文件的名称就只是包.文件名，没有后缀



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course58)



