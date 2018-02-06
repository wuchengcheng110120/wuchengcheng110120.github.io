## [上一页](course108)
##  【第16个代码模型】反射与代理设计模式（基础代理设计模式）

在实际的开发过程之中有两大核心设计模式：工厂设计模式、代理设计模式，其中对于工厂设计模式我们已经有了一个比较好的设计方案，但是代理设计模式我们没有一个很好的实现。现在就利用反射对之前的代理设计模式进行一个加强。

代理设计模式的核心本质在于：一个接口有两个子类：一个负责真实业务，另一个负责与真实业务有关的辅助性操作。那么按照这样一个原则，一个基础的代理设计结构如下：

	package cn.mldn.demo;
	
	import java.lang.reflect.Constructor;
	
	interface ISubject {//代理模式的核心在于需要有一个核心的操作接口
		public void eat();//吃饭是整体的核心业务
	}
	
	class RealSubject implements ISubject{
		@Override
		public void eat() {
			System.out.println("饿了一定要吃饭！");
		}
	}
	class Factory{
		private Factory(){}
		@SuppressWarnings("unchecked")
		public static <T>T getInstance(String className){
			T t = null;
			try {
				t = (T)Class.forName(className).newInstance();
			} catch (Exception e) {
				e.printStackTrace();
			} 
			return t;
		}
		@SuppressWarnings("unchecked")
		public static <T>T getInstance(String className,Object obj){
			T t = null;
			try {
				Constructor<?> cons = Class.forName(className).getConstructor(obj.getClass().getInterfaces()[0]);
				t = (T) cons.newInstance(obj);
			} catch (Exception e) {
				e.printStackTrace();
			} 
			return t;
		}
	}
	class ProxySubject implements ISubject{
		private ISubject subject;
		public ProxySubject(ISubject subject) {
			this.subject = subject;
		}
		public void prepare() {
			System.out.println("需要准备食材，收拾食材 ！");
		}
		public void eat() {
			this.prepare();
			this.subject.eat();
			this.clear();
		}
		public void clear() {
			System.out.println("洗刷碗筷 ！");
		}
	}
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			ISubject subject = Factory.getInstance("cn.mldn.demo.ProxySubject", Factory.getInstance("cn.mldn.demo.RealSubject"));
			subject.eat();
		} 	
	}

以上的程序结合了反射之后整体的处理会变得非常繁杂，而且繁杂的不只是开发端，而且用户端的调用也会非常繁琐，对于以上的操作客户端不应该关注特别多的内容。也就是说客户端唯一需要知道的就是代理是谁，真实操作是谁。所以程序可以这样修改。

**范例** 修改工厂类：

	package cn.mldn.demo;
	
	import java.lang.reflect.Constructor;
	
	interface ISubject {//代理模式的核心在于需要有一个核心的操作接口
		public void eat();//吃饭是整体的核心业务
	}
	
	class RealSubject implements ISubject{
		@Override
		public void eat() {
			System.out.println("饿了一定要吃饭！");
		}
	}
	class Factory{
		private Factory(){}
		@SuppressWarnings("unchecked")
		public static <T>T getInstance(String className){
			T t = null;
			try {
				t = (T)Class.forName(className).newInstance();
			} catch (Exception e) {
				e.printStackTrace();
			} 
			return t;
		}
		@SuppressWarnings("unchecked")
		public static <T>T getInstance(String ProxyClassName,String RealClassName){
			T t = null;
			try {
				T obj = getInstance(RealClassName); // 取得真实的接口对象
				Constructor<?> cons = Class.forName(ProxyClassName).getConstructor(obj.getClass().getInterfaces()[0]);
				t = (T) cons.newInstance(obj);
			} catch (Exception e) {
				e.printStackTrace();
			} 
			return t;
		}
	}
	class ProxySubject implements ISubject{
		private ISubject subject;
		public ProxySubject(ISubject subject) {
			this.subject = subject;
		}
		public void prepare() {
			System.out.println("需要准备食材，收拾食材 ！");
		}
		public void eat() {
			this.prepare();
			this.subject.eat();
			this.clear();
		}
		public void clear() {
			System.out.println("洗刷碗筷 ！");
		}
	}
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			ISubject subject = Factory.getInstance("cn.mldn.demo.ProxySubject", "cn.mldn.demo.RealSubject");
			subject.eat();
		} 	
	}

![](http://ww3.sinaimg.cn/large/0060lm7Tly1fo6y2o32j9j30vd0hb7av.jpg)

在开发中不知道一个项目会有多少个接口，那么如果所有的接口都要使用代理类会如何？按照这样的要求几乎每一个接口都要编写两个子类，那么假设所有接口的代理类的功能几乎都一样。

之前的这种代理设计严格来讲只是一种最简单的代理设计。所以这种代理设计只能够代理一个接口的子类对象，而不能代理多个接口的子类对象，那么这种开发是不可能在实际工作中出现的。



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course110)
