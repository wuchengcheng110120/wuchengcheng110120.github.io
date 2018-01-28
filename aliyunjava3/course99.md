## [上一页](course98)
##  反射与类操作（反射调用构造）

一个类中可以存在有多个构造方法，那么如果想要取得类中构造的调用，就可以使用Class类提供的两个方法：

- 取得指定参数类型的构造：public Constructor<T> getConstructor(Class<?>... parameterTypes)
                              throws NoSuchMethodException,
                                     SecurityException

- 取得类中的所有构造：public Constructor<?>[] getConstructors()
                                 throws SecurityException

以上两个方法返回的类型都是：java.lang.reflect.Constructor类的实例化对象，这个类里面关注一个方法:

- 实例化对象：public T newInstance(Object... initargs)
              throws InstantiationException,
                     IllegalAccessException,
                     IllegalArgumentException,
                     InvocationTargetException

**范例** 取得类中的所有构造方法信息：

	import java.lang.reflect.Constructor;
	
	class Person{
		private String name;
		private int age;
		
		public Person() {
		}
		public Person(String name) {
			this.name = name;
		}
		public Person(String name, int age) {
			this.name = name;
			this.age = age;
		}
		
	}
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			Class<?> cls = Person.class;
			Constructor<?> conts[] = cls.getConstructors();
			for (int x = 0; x < conts.length; x++) {
				System.out.println(conts[x]);
			}
		} 
	}
**console：**

	public cn.mldn.demo.Person()
	public cn.mldn.demo.Person(java.lang.String)
	public cn.mldn.demo.Person(java.lang.String,int)

以上操作是直接利用了Constructor类中的toString()方法取得了构造方法的完整信息，而如果只使用getName()方法就会比较麻烦了。

讲解Constructor类的目的并不是去分析构造方法的取得组成，重要的是之前一个问题的结论：

在定义简单Java类的时候一定要保留一个无参构造。

**范例** 观察Class实例化对象的问题

	class Person{
		private String name;
		private int age;
	
		public Person(String name, int age)throws Exception {
			this.name = name;
			this.age = age;
		}
	
		@Override
		public String toString() {
			return "Person [name=" + name + ", age=" + age + "]";
		}
	}
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			Class<?> cls = Person.class;
			System.out.println(cls.newInstance());
		} 
	}
**console：**

	Exception in thread "main" java.lang.InstantiationException: cn.mldn.demo.Person
		at java.lang.Class.newInstance(Unknown Source)
		at cn.mldn.demo.TestDemo.main(TestDemo.java:24)
	Caused by: java.lang.NoSuchMethodException: cn.mldn.demo.Person.<init>()
		at java.lang.Class.getConstructor0(Unknown Source)
		... 2 more

Class类通过反射实例化类对象的时候，只能够调用类中的无参构造。，那么如果现在类中没有无参构造，无法使用Class类操作，只能够通过明确的构造调用执行实例化处理：

**范例** 通过Constructor类实例化对象:

	import java.lang.reflect.Constructor;
	
	class Person{
		private String name;
		private int age;
	
		public Person(String name, int age)throws Exception {
			this.name = name;
			this.age = age;
		}
	
		@Override
		public String toString() {
			return "Person [name=" + name + ", age=" + age + "]";
		}
	}
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			Class<?> cls = Person.class;
			//现在明确表示取得指定参数类型的构造方法对象
			Constructor<?> cont = cls.getConstructor(String.class,int.class);
			System.out.println(cont.newInstance("张三",20));
		} 
	}
**console:**

	Person [name=张三, age=20]

结论：以后写简单Java类要写无参构造。



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course100)
