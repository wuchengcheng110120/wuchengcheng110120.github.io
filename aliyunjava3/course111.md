## [上一页](course110)
##  【第16个代码模型】反射与代理设计模式（cglib实现动态代理）

代理设计模式实现了，但是所有的代理设计模式都会存在有一个问题：离不开接口，也就是说所有代理模式的核心就是需要有接口，于是此时有人提出了一个疑问：不要接口，也要用代理设计，而且要搞动态代理设计。

这个要求最关键的因素在于需要实现没有接口的动态代理设计模式，那么需要清楚一点，代理类对象动态创建的语法：

Proxy.newProxyInstance(target.getClass().getClassLoader(), target.getClass().getInterfaces(), this) ;

那么此时如果要想实现这样的要求，就必须依靠另外的第三方组件包：cglib开发包，这个开发包可以帮助用户实现这类的需求，这个开发包是由：sourceforge.net（sf.net）提供的开发包，如果想要使用这个开发包，就必须将其配置到CLASSPATH之中。jar包中需要编译过的class文件而不是java文件

**范例** 实现基于类操作的动态代理：
	
	package cn.mldn.demo;
	
	import java.lang.reflect.Method;
	
	import net.sf.cglib.proxy.Enhancer;
	import net.sf.cglib.proxy.MethodInterceptor;
	import net.sf.cglib.proxy.MethodProxy;
	
	class Message{//直接做此类的代理
		public void send() {
			System.out.println("www.mldn.cn");
		}
	}
	class MyProxy implements MethodInterceptor {//定义一个拦截器
		private Object target; //代理的真实主题对象
		public MyProxy(Object target) {//直接通过构造方法传递进来
			this.target = target;
		}
		@Override
		public Object intercept(Object proxy, Method method, Object[] args, MethodProxy mProxy) throws Throwable {
			this.prepare();
			Object ret = method.invoke(this.target, args);
			this.over();
			return ret;
		}
		public void prepare() {
			System.out.println("【ProxySubject】打开电脑！");
		}
		public void over() {
			System.out.println("【ProxySubject】关闭电源！");
		}
	}
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			Message msg = new Message();
			Enhancer enhancer = new Enhancer(); //这是一个负责操作代理关系的程序类
			enhancer.setSuperclass(msg.getClass());//把本类的类型做一个描述
			enhancer.setCallback(new MyProxy(msg));  //代理对象
			// 以上就动态配置好了类之间的代理关系
			Message temp = (Message)enhancer.create();
			temp.send();
		} 	
	}

该设计属于反正规的代理设计，了解即可；

1、动态代理设计模式必须掌握，必须清楚每一个类和接口的作用以及彼此之间的联系

2、能够写动态代理类，了解cglib实现的特点


## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course112)
