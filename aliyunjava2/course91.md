## [上一页](course90)

## 【第04个代码模型】异常的捕获与处理（throw关键字）

throw是直接编写在语句之中的，表示人为进行异常的抛出。例如，在之前使用过一个10/0这样的语句，而这样的语句执行之后所产生的数学异常是由JVM负责进行异常类的实例化，而现在如果不希望异常类对象由系统产生，希望由用户来控制异常类实例化对象的产生，就可以使用throw来完成。

**范例** 使用throw产生异常类对象：

	public class TestDemo {
		public static void main(String[] args) {
				try {
					throw new Exception("老子就要抛，没事干");//实例化对象
				} catch (Exception e) {
					e.printStackTrace();
				}
		}
	}

一般而言throw和break、continue、return一样都需要结合if判断来使用。

throws和throw的区别：

- throw用于方法内部主要表示进行手工的异常抛出；

- throws主要在方法声明上使用，明确的告诉本方法可能产生的异常，同时该方法可能不处理此异常。




## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course92)
