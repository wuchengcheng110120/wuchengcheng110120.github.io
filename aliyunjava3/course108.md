## [上一页](course107)
##  ClassLoader类加载器（自定义类加载器）

希望可以通过一个程序来实现文件的类加载器。

**范例** 在D盘上建立一个Member.java文件：

	package cn.mldn.vo;
	
	class Member{// 自定义的类，这个类一定在CLASSPATH之中
		@Override
		public String toString() {
			return "是个人:Member";
		}
	}

随后要对此文件进行编译，但是不打包，javac Member.java，会形成Member.class文件。

现在希望通过自定义的类加载器实现D:\Member.class数据的加载。

**范例** 实现自定义类加载器:

- ClassLoader类定义的加载：

		protected final Class<?> defineClass(String name,
	  			 byte[] b,  int off, int len)  throws ClassFormatError

	package cn.mldn.demo;
	import java.io.ByteArrayOutputStream;
	import java.io.File;
	import java.io.FileInputStream;
	import java.io.InputStream;
	
	class MyClassLoader extends ClassLoader{
		/**
		 * 实现一个自定义类的加载器的操作，传入类的名称后，要通过指定的文件加载路径加载
		 * @param className 类的名称
		 * @return 返回类的Class对象
		 * @throws Exception
		 */
		public Class<?> loadData(String className)throws Exception{
			byte classData []  = this.loadClassData(); // 加载类文件的数据信息
			return super.defineClass(className, classData, 0, classData.length);
		}
		/**
		 * 通过指定的文件路径进行类的文件加载，就是进行二进制读取
		 * @return 类文件数据
		 * @throws Exception
		 */
		private byte [] loadClassData() throws Exception{
			InputStream input  = new FileInputStream(new File("D:" + File.separator + "Member.class" ));
			ByteArrayOutputStream bos = new ByteArrayOutputStream(); //可以有一个方法取得所有字节的内容
			byte data[] = new byte[20]; //定义读取的缓冲区大小
			int temp = 0;
			while ((temp = input.read(data)) != -1) {
				bos.write(data, 0, temp);
			}
			byte ret[] =bos.toByteArray();
			input.close();
			bos.close();
			return ret;
		}
	}
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			Class<?> cls = new MyClassLoader().loadData("cn.mldn.vo.Member");
			System.out.println(cls.newInstance());
			System.out.println(cls.getClassLoader());
			System.out.println(cls.getClassLoader().getParent());
			System.out.println(cls.getClassLoader().getParent().getParent());
		} 
	}
**console：**

	是个人:Member
	cn.mldn.demo.MyClassLoader@25154f
	sun.misc.Launcher$AppClassLoader@139a55
	sun.misc.Launcher$ExtClassLoader@647e05
	
类加载器给用户最大的帮助在于可以通过动态的路径实现类的加载处理操作。

大部分情况下不需要自己实现类加载，但是需要清楚类加载流程。



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course109)
