## [上一页](course94)

## 【第04个代码模型】异常的捕获与处理（自定义异常类）

在Java里面实际上针对于可能出现的公共的程序问题，都会提供有相应的异常信息，但是很多时候这些异常信息往往不够我们使用，例如：现在在进行加法处理的时候，如果发现两个内容的相加结果为30，那么就应该抛出一个AddException的异常，但是这种异常Java是不会提供的，所以就必须定义一个属于自己的异常类，如果要想定义属于自己的异常类可以继承两种父类：Exception、RuntimeException。

**范例** 实现自定义异常类：

	class AddException extends Exception{
		public AddException(String msg) {
			super(msg);
		}
	}
	public class TestDemo {
		public static void main(String[] args) throws Exception{
				if (10 + 20 == 30) {
					throw new AddException("错误的相加操作！ ");
				}
		}
	}

**console：**

	Exception in thread "main" bznoc171118.AddException: 错误的相加操作！ 
		at bznoc171118.TestDemo.main(TestDemo.java:10)

一般如果做项目系统设计的时候，一定会牵扯到业务相关的异常问题，有错误Google、stackoverflow.com

对于异常处理不需要刻意使用，目前需要知道：

- 异常的处理流程；

- 异常的处理格式；

- 异常处理模型；



## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course96)
