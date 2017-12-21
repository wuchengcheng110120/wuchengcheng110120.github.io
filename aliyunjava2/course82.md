## [上一页](course81)

## 包的定义及使用（包的导入）

开发之中一旦使用了包的定义，实际上就相当于把一个大的项目分别按照一定的保存在了不同的包里面（不同的文件夹里面），但是这些程序类彼此之间一定会发生互相调用的情况，所以这种时候就要采用导入包的处理方式。

**范例** 编写一个简单的程序类，本类将被其他程序导入：

	package cn.mldn.util;
	public class Message 
	{
		public void print(){
			System.out.print("【Message】 Hello World ！");
		}
	}

注意：类使用class和 public class的一个区别？

- public class：文件名称必须与类名称保持一致，如果希望一个类被其它包所访问，则必须定义为public class

- class：文件名称可以与类名称不一致，在一个*.java中可以定义多个class，但是这个类不允许被其他包所访问

**范例** 希望通过不同的包导入以上的程序类：

	package cn.mldn.test;
	import cn.mldn.util.Message;//导入程序类
	
	public class Mytest
	{
		public static void main(String[] args) 
		{
			Message msg = new Message();
			Message.print();
		}
	}

从正常的角度来讲，Mytest类去引用了Message类，那么首先编译的就是Message类，而后才是Mytest类。如果都按照这样的顺序进行编译后果是可怕的，所以最好的做法是让java自己去匹配先后顺序，最常用的打包编译：javac -d .*.java；

另外需要注意一点，在在上面的程序之中导入的时候采用的是“import 包.类”，这样只会导入一个类，如果说现在要想导入一个包中的多个类，建议可以直接采用通配符“*”来完成。

		import cn.mldn.util.*;//导入程序类

这种“*”并不表示将所有的类都导入，而是根据你的需求进行导入。

但是在很多的开发情况中，也很可能出现不同包但是相同类的情况。假设建立一个新的Message.class文件。

**范例** 不同包相同类：

	package cn.apache.util;
	public class Message 
	{
		public void info(){
			System.out.print("【Message】 世界和平 ！");
		}
	}

现在由于某种需求MyTest程序类里面需要同时导入这两个包；

那么这个时候如果你还是直接使用Message类就会造成，编译上的歧义。

	package cn.mldn.test;
	import cn.mldn.util.*;//导入程序类
	import cn.apache.util.*;
	public class Mytest
	{
		public static void main(String[] args) 
		{
			Message msg = new Message();
			msg.print();
		}
	}

javac -d . Mytest.java 出现错误

那么此时最好的做法是明确的导入所需要的包.类；或者直接在使用的类上采用全名的方式定义；

	package cn.mldn.test;
	import cn.mldn.util.*;//导入程序类
	import cn.apache.util.*;
	public class Mytest
	{
		public static void main(String[] args) 
		{
			cn.mldn.util.Message msg = new cn.mldn.util.Message();
			msg.print();
		}
	}

javac -d . Mytest.java

java cn.mldn.test.Mytest

**console:**

	Hello World!

以后的开发之中这类的情况一定会出现，如果出现了请使用全名。

## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course83)
