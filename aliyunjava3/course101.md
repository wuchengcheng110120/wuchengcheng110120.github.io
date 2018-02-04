## [上一页](course100)
##  反射与类操作（反射调用成员）

之前已经成功的实现了类的构造调用、方法调用，那么除了这两种模式以外还需要有成员调用。前提：类中的所有属性一定要在类对象实例化之后才会进行空间分配，所以此时想要调用类的属性，必须保证有实例化对象，通过反射的newInstance()方法可以直接取得实例化对象（Object类型）。

在Class类里面提供有两组取得属性的操作方法：

- 取得父类属性：

	|- 取得类中的全部属性：  
		
		public Field[] getFields()
                  throws SecurityException

	|- 取得类中指定名称的属性： 

		 public Field getField(String name)
               throws NoSuchFieldException,
                      SecurityException

- 取得本类属性：

	|- 取得类中的全部属性：

		public Field[] getDeclaredFields()
                          throws SecurityException
		
	|- 取得类中指定名称的属性：

		public Field getDeclaredField(String name)
                       throws NoSuchFieldException,
                              SecurityException

**范例** 取得类中的全部属性：

		package cn.mldn.demo;
		
		import java.lang.reflect.Field;
		
		class Person{
			public String name;//此时的类中只是明确的提供有一个属性
		}
		class Student extends Person{
			private String school;
		}
		public class TestDemo {
			public static void main(String[] args) throws Exception {
				Class<?> cls = Class.forName("cn.mldn.demo.Student");
				{//普通代码块
					Field fields [] = cls.getFields();//取得全部属性
					for (int x = 0; x < fields.length; x++) {
						System.out.println(fields[x]);
					}
				}
				System.out.println("--------------------------");
				{//普通代码块
					Field fields [] = cls.getDeclaredFields();//取得全部属性
					for (int x = 0; x < fields.length; x++) {
						System.out.println(fields[x]);
					}
				}
			} 
		}

**console：**

	public java.lang.String cn.mldn.demo.Person.name
	--------------------------
	private java.lang.String cn.mldn.demo.Student.school

因为在实际的开发之中，属性基本上都会进行封装处理，所以自然没有必要去关注父类中的属性，也就是说以后操作中所取得的属性都以本类属性为主。

而后现在需要关注属性的核心描述类：

java.lang.reflect.Field

在这个类里面有两个重要的方法：

- 设置属性内容：

		public void set(Object obj,
                Object value)
         throws IllegalArgumentException,
                IllegalAccessException

- 取得属性内容：

		public Object get(Object obj)
           throws IllegalArgumentException,
                  IllegalAccessException

![](http://ww4.sinaimg.cn/large/0060lm7Tly1fo48dlm55ij30vd0hetf8.jpg)

![](http://ww4.sinaimg.cn/large/0060lm7Tly1fo48dlm55ij30vd0hetf8.jpg)

在java.lang.reflect.AccessibleObject类中提供有一个方法：

- 动态设置封装：public void setAccessible(boolean flag)
                   throws SecurityException

**范例** 通过反射操作属性：

	package cn.mldn.demo;
	
	import java.lang.reflect.Field;
	
	class Person{
		private String name;//此时的类中只是明确的提供有一个属性
	}
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			Class<?> cls = Class.forName("cn.mldn.demo.Person");
			Object obj = cls.newInstance();//实例化本类对象
			Field nameField = cls.getDeclaredField("name");//操作name属性
			nameField.setAccessible(true);
			nameField.set(obj, "张三");//等价于：对象.name = 张三
			System.out.println(nameField.get(obj));
		} 
	}
**console：**

	张三

但是如果在实际的开发之中使用更多的属性操作绝对不可能直接按照如上的模式进行，一定要使用setter和getter方法，因为可以给用户操作的机会。

在Field类里面有一个特别有用的方法：

- 取得属性类型：public Class<?> getType()

		package cn.mldn.demo;
		
		import java.lang.reflect.Field;
		
		class Person{
			private String name;//此时的类中只是明确的提供有一个属性
		}
		
		public class TestDemo {
			public static void main(String[] args) throws Exception {
				Class<?> cls = Class.forName("cn.mldn.demo.Person");
				Object obj = cls.newInstance();//实例化本类对象
				Field nameField = cls.getDeclaredField("name");//操作name属性
				System.out.println(nameField.getType().getName());//包，类
				System.out.println(nameField.getType().getSimpleName());//类名称
			} 
		}

**console：**

	java.lang.String
	String

将Field取得属性与Method类中的invoke()结合在一起，就可以编写非常灵活的程序了。



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course102)
