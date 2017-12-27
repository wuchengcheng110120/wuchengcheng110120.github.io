## [上一页](course92)

## 【第04个代码模型】异常的捕获与处理（RuntimeException）

在讲解之前先看一段简单的程序；

	public class TestDemo {
		public static void main(String[] args) {
				String str = "100";
				int num = Integer.parseInt(str);
				System.out.println(num * 2);
		}
	}


于是来观察以下Integer类中关于parseInt（）方法的定义：

public static int parseInt(String s)throws NumberFormatException

这个方法上已经明确的抛出了一个异常，但是在调用的时候发现即使没有进行异常处理，也可以正常执行，这个就属于RuntimeException的范畴了，来观察NumberFormatException的继承结构：

	java.lang.Object
	  |-java.lang.Throwable
		|-java.lang.Exception
		  |-java.lang.RuntimeException
			|-java.lang.IllegalArgumentException
			  |-java.lang.NumberFormatException

很多的代码上都可能产生异常，例如：数学计算“10/0”，都可能会产生异常，如果所有可能产生异常的地方都要求进行强制性的异常处理，代码过于复杂，所以在异常设计的时候考虑到一些异常可能是很简单的问题，所以将这类的异常统一称为RuntimeException，也就是说使用RuntimeException定义的异常类可以不需要强制性进行异常处理。

Exception与RuntimeException的区别：

- Exception是RuntimeException的父类，使用Exception定义的异常都要求使用异常处理：

- 而RuntimeException可以由用户选择性地进行异常处理

列举出几个常见的RuntimeException：

- ArithmeticException、 NullPointerException；





## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course94)
