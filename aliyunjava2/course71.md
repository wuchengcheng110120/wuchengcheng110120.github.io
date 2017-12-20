## [上一页](course70)

## 接口的定义与使用（代理设计模式）

### Proxy模式

所谓的代理严格来讲就是两个子类共同实现一个接口，其中一个子类负责真实的业务实现，而另外的子类负责完成辅助真实业务主题的操作。

![](https://i.imgur.com/BeeNb6e.png)

**范例** 实现代理设计：

	interface ISubject{//
		public void save();      //核心功能是救人
	}
	class RealSubject implements ISubject{
		public void save() {
			System.out.println("英勇的制止了于先生马上进行的不法侵害。");
		}
	}
	class ProxySubject implements ISubject{//代理实现
		private ISubject subject;//真正的操作业务
		//在创建代理类对象的时候必须设置要代理的真实主题
		public ProxySubject(ISubject subject) {
			this.subject = subject;
		};
		public void broke() {
			System.out.println("1、 破门而入！ ");
		}
		public void get() {
			System.out.println("2、 得到见义勇为奖！ ");
		}
		public void save() {//接口子类一定要实现抽象方法
			this.broke();//操作前的准备
			this.subject.save();//调用真实的业务
			this.get();//操作后的收尾
		}
	}
	class Factory {
		public static ISubject getInstance() {
			return new ProxySubject(new RealSubject());
		}
	}
	public class TestDemo {
		public static void main(String[] args) {
			ISubject sub = Factory.getInstance();
			//通过代理类对象发出，利用代理类来实现真实业务调用
			sub.save();//救人操作
		}
	}

**console：**

	1、 破门而入！ 
	英勇的制止了于先生马上进行的不法侵害。
	2、 得到见义勇为奖！ 

不过对于初次接触代理模式的同学来讲有一些抽象。

代理的本质：所有的真实业务操作都会有一个与之辅助的功能类共同完成。




## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course72)
