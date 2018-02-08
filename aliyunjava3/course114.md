## [上一页](course113)
##   反射与Annotation（Annotation与工厂设计模式）

之前的工厂类设计模式都是通过明确的类信息传递实现的实例化对象。

	package cn.mldn.demo;
	
	import java.io.Serializable;
	import java.lang.annotation.Annotation;
	import java.lang.annotation.Retention;
	import java.lang.annotation.RetentionPolicy;
	
	interface IFruit{
		public void eat();
	}
	class Apple implements IFruit{
		@Override
		public void eat() {
			System.out.println("吃苹果！");
		}
	}
	@MyAnnotation(target = Apple.class)
	class Factory{
		@SuppressWarnings("unchecked")
		public static <T> T getInstance() throws Exception{
			MyAnnotation ant = Factory.class.getAnnotation(MyAnnotation.class);
			return (T) ant.target().newInstance();
		}
	}
	
	@Retention(RetentionPolicy.RUNTIME) // 表示此Annotataion在运行时生效
	@interface MyAnnotation{
		public Class<?> target(); // 定义的是实例化子类的类型
	}
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			IFruit fruit = Factory.getInstance(); // 没有传递参数
			fruit.eat();
		} 	
	}
**console：**

	吃苹果！

通过观察代码可以发现Annotation已经很好的解决了当前的一个配置项的问题，也就是说程序可以通过配置的Annotation的信息来实现不同的操作效果。

对于Annotation的开发，大概了解就可以，暂时不将其作为重点，以后会使用到许多开发框架提供的Annotation的标记。

## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course115)
