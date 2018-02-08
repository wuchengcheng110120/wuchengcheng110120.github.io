## [上一页](course111)
##   反射与Annotation（反射取得Annotation）

Annotation这项技术可以说是颠覆性的开发技术，也就是说在以后的开发中会接触到大量的Annotation，Annotation如果要想设计必须有一个前提，需要有一个代码容器才可以实现自定义的Annotation。

Annotation的注解可以定义在类或方法上，而且现在也知道有反射的概念，此时最好的做法是可以通过反射取得所定义的Annotation信息。

在java.lang.reflect.AccessibleObject(java.lang.Class<T>)中提供有与Annotation有关的方法：

- 取得全部的Annotation：public Annotation[] getAnnotations()

- 取得指定的Annotation: public <T extends Annotation> T getAnnotation(Class<T> annotationClass)

**范例** 取得定义在类上的Annotation：

	import java.io.Serializable;
	import java.lang.annotation.Annotation;
	
	@SuppressWarnings("serial")
	@Deprecated
	class Member implements Serializable{}
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			Annotation ant[] =  Member.class.getAnnotations();
			for (int x = 0; x < ant.length; x++) {
				System.out.println(ant[x]);
			}
		} 	
	}
**console：**

	@java.lang.Deprecated()

Annotation有自己的保存范围，不同的Annotation有不同的保存范围。所以此处才出现了一个Annotation的信息。

**范例** 在方法上使用Annotation：

	import java.io.Serializable;
	import java.lang.annotation.Annotation;
	
	@SuppressWarnings("serial")
	
	class Member implements Serializable{
		@Override
		@Deprecated
		public String toString() {
			return super.toString();
		}
	}
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			Annotation ant[] =  Member.class.getMethod("toString").getAnnotations();
			for (int x = 0; x < ant.length; x++) {
				System.out.println(ant[x]);
			}
		} 	
	}
**console：**

	@java.lang.Deprecated()

反射可以取得结构定义的Annotation，所以所谓的Annotation的设计是不可能离开反射的。




## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course113)
