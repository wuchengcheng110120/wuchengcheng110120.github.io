## [上一页](course44)

##  static关键字（分析主方法）

如果一个方法定义在主类之中并且由主方法直接调用，那么该方法的定义语法如下：

public static 返回值类型 方法名称（参数列表）{}

后来写到类结构的时候并没有使用static，其中主要原因也是因为static的限制

	public class TestDemo {
		public static void main(String args[]) {//static方法
			print();
		}
		public static void print() {//static 方法
			System.out.println("Hello World ! ");
		}
	}

如果此时print（）方法上没有写static关键字，那么表示的就是非static方法，所有的非static方法必须通过类对象才可以使用。

	public class TestDemo {
		public static void main(String args[]) {//static方法
			new TestDemo().print();;
		}
		public void print() {//static 方法
			System.out.println("Hello World ! ");
		}
	}

反过来看必须清楚一个问题，java中给出的主方法的名字是最长的，其组成意义如下

- public：表示公共的，主方法作为起点，必须可以访问

- static：执行java程序的时候执行的是一个类名称，表示不受实例化对象限制

- void：主方法是一切的起点，既然开始了就走吧；

- main：是一个系统定义好的方法名称；

- String args[] ：表示该类执行时所需要的相关参数。

**范例** 取得执行参数：

	public class TestDemo {
		public static void main(String args[]) {
			//所有的参数类型都是String型
			for (int i = 0; i < args.length; i++) {
				System.out.println(args[i]);
			}
		}
	}

run->run configurations-> 

![](https://i.imgur.com/enjyRjy.png)

在这个位置设置args[]



## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course46)
