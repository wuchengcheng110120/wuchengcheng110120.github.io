## [上一页](course109)
##  【第16个代码模型】反射与代理设计模式（动态代理设计模式）

动态代理设计模式的核心特点：一个代理类可以代理所有需要被代理的接口的子类对象。

![](http://ww3.sinaimg.cn/large/0060lm7Tly1fo7sp1z8moj30v80hh7d5.jpg)

如果想要进行动态代理设计的实现，代理类不再具体实现于某一个接口

	public interface InvocationHandler {
		/**
		 * invoke() 表示调用执行的方法，但是所有代理类返回给用户的接口的对象都属于代理对象
		 * 当用户执行接口方法的时候所调用的实例化对象就是该代理主题动态创建的一个接口对象
		 * @param proxy 表示的是被代理的对象信息
		 * @param method 返回的是被调用的方法对象，取得了Method对象意味着可以使用invoke()反射调用方法
		 * @param args 表示方法中接收到的参数
		 * @return 方法的返回值
		 * @throws Throwable 可能产生各种类型的Exception或Error
		 */
		public Object invoke(Object proxy, Method method,Object[] args) throws Throwable;
	}

如果想要进行对象的绑定，那么就需要使用到一个Proxy()的程序类，这个程序类的主要功能是可以绑定所有的你需要绑定的接口子类的对象，而且这些对象都是根据接口自动创建的。该类中有一个动态创建对象绑定的方法：

- public static Object newProxyInstance(ClassLoader loader,
                                      Class<?>[] interfaces,
                                      InvocationHandler h)
                               throws IllegalArgumentException

**范例** 动态代理模式实现

		package cn.mldn.demo;
		
		import java.lang.reflect.InvocationHandler;
		import java.lang.reflect.Method;
		import java.lang.reflect.Proxy;
		import java.util.Arrays;
		
		interface ISubject {//代理模式的核心在于需要有一个核心的操作接口
			public void eat(String msg, int num);//吃饭是整体的核心业务
		}
		
		class RealSubject implements ISubject{
			@Override
			public void eat(String msg, int num) {
				System.out.println("我要吃" + num + "份" + msg);
			}
		}
		
		
		class ProxySubject implements InvocationHandler{//是一个动态代理类
			private Object target; // 绑定任意的接口的对象，使用Object描述
			/**
			 * 实现真实对象的绑定处理，同时返回代理对象
			 * @param target
			 * @return 返回一个代理对象（这个对象是根据接口定义动态创建形成的代理对象）
			 */
			public Object bind(Object target) {
				this.target = target; //保存真实主题对象
				return Proxy.newProxyInstance(target.getClass().getClassLoader(), target.getClass().getInterfaces(), this) ;
			}
			public void prepare() {
				System.out.println("【ProxySubject】 准备食材！");
			}
			public void clear() {
				System.out.println("【ProxySubject】 收拾碗筷！");
			}
			@Override
			public Object invoke(Object proxy, Method method, Object[] args) throws Throwable {
		//		System.out.println(proxy.getClass());
		//		System.out.println(method);
		//		System.out.println(Arrays.toString(args));
				this.prepare();
				Object ret = method.invoke(this.target, args); // 反射调用方法
				this.clear();
				return ret;
			}
		}
		
		public class TestDemo {
			public static void main(String[] args) throws Exception {
				ISubject subject =(ISubject) new ProxySubject().bind(new RealSubject());
				subject.eat("鱼香肉丝", 20);
			} 	
		}

如果还想要进一步实现，就需要使用工厂类对实例化接口对象部分做进一步的隐藏处理。



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course111)
