## [上一页](course97)
##  反射与类操作（取得父类信息）

利用反射可以做出一个对象的所有操作行为，而且最关键的是这一切的操作都可以基于Object类型进行。

在Java里面所有的类实际上都有父类，在Class类里面就可以通过此方式来获得父类或者实现的父接口，有如下的两个方法：

- 取得类的包名称：public Package getPackage()；

- 取得父类的Class对象： public Class<? super T> getSuperclass()

- 取得父接口对象：public Class<?>[] getInterfaces()

	interface IFruit {}
	interface IMessage{}
	class Person implements IMessage,IFruit{}
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			Class<?> cls = Person.class;
			System.out.println(cls.getPackage().getName());
			System.out.println(cls.getSuperclass().getName());
			Class<?> itf[] = cls.getInterfaces();
			for (int i = 0; i < itf.length; i++) {
				System.out.println(itf[i].getName());
			}
		} 
	}
**console：**

	cn.mldn.demo
	java.lang.Object
	cn.mldn.demo.IMessage
	cn.mldn.demo.IFruit

通过反射可以取得类结构中的关键信息。

## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course99)
