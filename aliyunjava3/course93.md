## [上一页](course92)
##  【第13个代码模型】对象序列化（序列化实现）

如果想要实现序列化和反序列化的对象操作，在java.io提供有两个处理类：ObjectOutputStream、ObjectInputStream，来观察这两个类的定义结构以及各自的构造方法：

- ObjectOutputStream：

		public class ObjectOutputStream
		extends OutputStream
		implements ObjectOutput, ObjectStreamConstants
		
		java.lang.Object
		java.io.OutputStream
		java.io.ObjectOutputStream

构造方法：public ObjectOutputStream(OutputStream out)
                   throws IOException

public final void writeObject(Object obj)
                       throws IOException

![](http://ww3.sinaimg.cn/large/0060lm7Tly1fnu3zywr1xj30v80hg0y8.jpg)

- ObjectInputStream：
		
		public class ObjectInputStream
		extends InputStream
		implements ObjectInput, ObjectStreamConstants

		java.lang.Object
		java.io.InputStream
		java.io.ObjectInputStream

构造方法： public ObjectInputStream(InputStream in)
                  throws IOException

![](http://ww2.sinaimg.cn/large/0060lm7Tly1fnu418n4e1j30vd0hgjw7.jpg)

**范例** 实现对象序列化：

	import java.io.File;
	import java.io.FileInputStream;
	import java.io.FileOutputStream;
	import java.io.ObjectInputStream;
	import java.io.ObjectOutputStream;
	import java.io.Serializable;
	
	@SuppressWarnings("serial")
	class Person implements Serializable{
		private String name;
		private int age;
		public Person(String name, int age) {
			super();
			this.name = name;
			this.age = age;
		}
		public String getName() {
			return name;
		}
		public void setName(String name) {
			this.name = name;
		}
		public int getAge() {
			return age;
		}
		public void setAge(int age) {
			this.age = age;
		}
		@Override
		public String toString() {
			return "Person [name=" + name + ", age=" + age + "]";
		}
	}
	
	public class TestDemo {
		public static final File FILE  = new File("d:" + File.separator + "person.ser");
		public static void main(String[] args) throws Exception {
			ser(new Person("张三", 20));
			dser();
		} 
		public static void ser(Object obj) throws Exception{
			ObjectOutputStream oss = new ObjectOutputStream(new FileOutputStream(FILE));
			oss.writeObject(obj);
			oss.close();
		}
		public static void dser() throws Exception {
			ObjectInputStream ois = new ObjectInputStream(new FileInputStream(FILE));
			System.out.println(ois.readObject());
			ois.close();
		}
	}
**console：**

	Person [name=张三, age=20]

在之后的项目开发中，根本不需要知道序列化和反序列化操作，因为会有容器自动处理。


## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course94)
