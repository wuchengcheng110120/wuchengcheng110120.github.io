## [上一页](course95)
##  Class类对象的三种实例化模式

Class类是描述整个类的概念，所以也是整个反射操作的源头

	java.lang.Object
	java.lang.Class<T>

	public final class Class<T>
	extends Object
	implements Serializable, GenericDeclaration, Type, AnnotatedElement

那么在使用Class类的时候需要关注的依然是这个类的对象，而这个类的对象的产生模式一共有三种：

- 任何的实例化对象可以通过Object类中的getClass()方法获得Class类对象：

	import java.util.Date;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			Class<?> cls = new Date().getClass();
			System.out.println(cls.getName());
		} 
	}

- “类.class”：直接根据一个具体的类来取得Class类的实例化对象：

	import java.util.Date;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			Class<?> cls = Date.class;
			System.out.println(cls.getName());
		} 
	}

- 使用Class类中提供的方法：public static Class<?> forName(String className)
                        throws ClassNotFoundException：

	public class TestDemo {
		public static void main(String[] args) throws Exception {
			Class<?> cls = Class.forName("java.util.Date");
			System.out.println(cls.getName());
		} 
	}

在以上给出的三个方法里面我们会发现一个神奇的地方：除了第一种形式会产生Date类的实例化对象之外，其它的两种都不会产生类的实例化对象。于是取得了Class类对象有一个好处：可以直接通过反射实例化对象，在Class类里面定义有如下一个方法：public T newInstance()
              throws InstantiationException,
                     IllegalAccessException

**范例** 反射实例化对象：

	public class TestDemo {
		public static void main(String[] args) throws Exception {
			Class<?> cls = Class.forName("java.util.Date");
			Object obj = cls.newInstance();//实例化对象，等价于new java.util.Date()
			System.out.println(obj);
		} 
	}
**console：**

	Fri Jan 26 18:00:03 CST 2018

那么现在发现除了关键字new之外对于对象的实例化模式有了第二种做法，通过反射进行。

取得了Class类对象就意味着取得了一个指定类的操作权。


## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course97)
