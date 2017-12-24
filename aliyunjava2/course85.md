## [上一页](course84)

## jar命令

现在的电脑使用中往往会将许多相关联的文件为了储存方便，以及节约空间都会将其放在压缩文件里面。实际上jar也是一种压缩文件，只不过里面保存的都是*.class文件，也就是说如果现在要实现某一个功能模块，可能有几百个，那么最终交付给用户使用的时候为了方便管理，就会将这些文件形成一个压缩包提供给用户。

在jdk之中提供有实现jar文件操作的命令，只需要输入一个jar即可。对于此命令有如下几个常用参数：

- “c”： 创建一个新的归档文件；

- “f”： 指定生成的jar文件的名称；

- “v”： 详细显示出所有的压缩处理过程；

**范例** 定义一个Message的程序类

	package cn.mldn.util;
	public class Message 
	{
		public void print(){
			System.out.print("【Message】 Hello World ！");
		}
	}

随后需要将其进行编译而后变为jar文件使用：

- 打包进行程序的编译

- 将生成的程序类打包成jar文件；

	|- 此文件可以通过winrar工具打开，而且打开之后会发现有一个META-INF目录

此时的my.jar就包含了所需要使用到的程序类；删除原cn文件；

但是要想使用这个jar文件，并不是将其放到程序的目录之中就可以的，还需要为其配置CLASSPATH，设置你的jar文件的加载路径才会起效；

**范例** 编写一个程序，调用my.jar包中提供的Message类：

	package cn.mldn.test;
	public class Mytest
	{
		public static void main(String[] args) 
		{
			cn.apache.util.Message msg = new cn.apache.util.Message();
			msg.info();
		}
	}

SET CLASSPATH=.;G:\my.jar;

以后的开发会使用大量的jar文件。开发中会使用大量的第三方程序包，这些开发包都必须在CLASSPATH中进行配置后才可使用，不进行配置是无法使用的；






## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course86)
