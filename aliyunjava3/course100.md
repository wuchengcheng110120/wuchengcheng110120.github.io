## [上一页](course99)
##  反射与类操作（反射调用方法）

实际上类中的构造方法的反射调用可能永远不会编写。但是类中的普通方法的反射调用在开发中一定会使用到，并且使用好可以省去大量的重复编码，在Class类中有如下两个取得类中普通方法的定义：

- 取得全部方法：public Method[] getMethods()
                    throws SecurityException

- 取得指定的方法： public Method getMethod(String name,
                        Class<?>... parameterTypes)
                 throws NoSuchMethodException,
                        SecurityException

以上两个方法返回的是java.lang.reflect.Method类的对象，在此类中提供有一个调用的方法支持：

	public Object invoke(Object obj,
	                     Object... args)
	              throws IllegalAccessException,
	                     IllegalArgumentException,
	                     InvocationTargetException

**范例** 取得一个类中的所有方法：

	import java.lang.reflect.Method;
	
	class Person{
		private String name;
		public String getName() {
			return name;
		}
		public void setName(String name) {
			this.name = name;
		}
		public void print() {}
	}
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			Class<?> cls = Person.class;
			Method met[] = cls.getMethods();//取得全部方法
			for (int i = 0; i < met.length; i++) {
				System.out.println(met[i]);
			}
		} 
	}
**console：**

	public java.lang.String cn.mldn.demo.Person.getName()
	public void cn.mldn.demo.Person.setName(java.lang.String)
	public void cn.mldn.demo.Person.print()
	public final void java.lang.Object.wait() throws java.lang.InterruptedException
	public final void java.lang.Object.wait(long,int) throws java.lang.InterruptedException
	public final native void java.lang.Object.wait(long) throws java.lang.InterruptedException
	public boolean java.lang.Object.equals(java.lang.Object)
	public java.lang.String java.lang.Object.toString()
	public native int java.lang.Object.hashCode()
	public final native java.lang.Class java.lang.Object.getClass()
	public final native void java.lang.Object.notify()
	public final native void java.lang.Object.notifyAll()

在之前所编写的程序对于Setter和Getter方法采用的都是明确的对象调用。

		Person pr = new Person();
		pr.setName("abc");
		System.out.println(pr.getName())

而现在有了反射机制处理之后，这个时候的程序即使没有明确的Person类型的对象（依然需要实例化对象，Object描述，所有的普通方法必须在有实例化对象之后才可以进行调用）。就可以通过反射来完成。

**范例** 通过反射调用setter和getter：

	package cn.mldn.demo;
	
	import java.lang.reflect.Method;
	
	class Person{
		private String name;
		public String getName() {
			return name;
		}
		public void setName(String name) {
			this.name = name;
		}
		public void print() {}
	}
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			String attribute = "name";//明确调用属性名称
			String value = "MLDN";//明确设置内容
			Class<?> cls = Class.forName("cn.mldn.demo.Person");
			Object obj = cls.newInstance();//任何情况下调用普通方法都必须实例化
			//取得setName这个方法的实例化对象
			//setName()是方法名称，但是这个方法名称是根据给定的属性信息拼凑得来的，同时该方法需要接收一个String型的参数
			Method setMethod = cls.getMethod("set"+initcap(attribute),String.class);
			//随后需要通过Method类对象调用指定的方法，调用方法必须有实例化对象，同时要传入一个参数
			setMethod.invoke(obj, value);//相当于Person对象.setName(value)
			Method getMethod = cls.getMethod("get"+initcap(attribute));
			Object ret = getMethod.invoke(obj);//相当于Person对象.getName(value)
			System.out.println(ret);
		} 
		public static String initcap(String str) {
			return str.substring(0, 1).toUpperCase() + str.substring(1);
		}
	}
**console：**

	MLDN

此类操作的好处是不再局限于某一具体类型的对象，而是可以通过Object类型进行所有类的方法调用。

## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course101)
