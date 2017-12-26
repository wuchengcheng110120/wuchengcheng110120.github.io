## [上一页](course88)

## 【第04个代码模型】异常的捕获与处理（trycatch关键字）

为了保证程序出现了错误之后仍然能够正常运行，那么就可以使用异常处理的操作，处理的语法格式如下：

	try{
			有可能出现异常的语句；
	}[catch（异常类 对象）]{
			异常的处理语句；
	}catch（异常类 对象）{
			异常的处理语句；
	}...][
	finally{
		异常的统一出口；
	}]

对于以上的三个关键字可以出现的组合：try...catch、try...finally、try...catch...finally。

**范例** 对异常进行处理：

	public class TestDemo {
		public static void main(String[] args) {
			System.out.println("【1】数学计算开始前");
			try {
				System.out.println("【2】数学计算: " + (10/0));
			} catch (ArithmeticException e) {
				System.out.println("【CATCH】 异常已经被处理了");
			}
			System.out.println("【3】数学计算结束后");
		}
	}

**console：**

	【1】数学计算开始前
	【CATCH】 异常已经被处理了
	【3】数学计算结束后

发现出现了异常之后，整个的程序由于存在有异常处理机制，那么依然可以正常的执行完毕。

以上的代码虽然进行了异常处理，但是这里面会存在有一个严重的问题，也就是说你现在根本不知道你的程序产生了什么样的异常，所以为了明确的取得异常的的信息，可以直接输出异常类对象，或者调用所有异常类中提供的printStackTrace（）方法进行完整异常信息的输出。

**范例** 取得异常的完整信息:

	public class TestDemo {
		public static void main(String[] args) {
			System.out.println("【1】数学计算开始前");
			try {
				System.out.println("【2】数学计算: " + (10/0));
			} catch (ArithmeticException e) {
				e.printStackTrace();
			}
			System.out.println("【3】数学计算结束后");
		}
	}

**console：**

	【1】数学计算开始前
	【3】数学计算结束后
	java.lang.ArithmeticException: / by zero
		at bznoc171118.TestDemo.main(TestDemo.java:9)

在进行异常处理的时候还可以使用try...catch..finally来进行操作处理。

**范例** 观察try...catch..finally操作：

	public class TestDemo {
		public static void main(String[] args) {
			System.out.println("【1】数学计算开始前");
			try {
				System.out.println("【2】数学计算: " + (10/0));
			} catch (ArithmeticException e) {
				e.printStackTrace();
			}finally {
				System.out.println("【FINALLY】 不管是否有异常都一定要执行此语句。");
			}
			System.out.println("【3】数学计算结束后");
		}
	}

**console：**

	【1】数学计算开始前
	【FINALLY】 不管是否有异常都一定要执行此语句。
	【3】数学计算结束后
	java.lang.ArithmeticException: / by zero
		at bznoc171118.TestDemo.main(TestDemo.java:9)

不管是否产生有异常，最终都要执行finally程序代码，所以finally会作为程序的统一出口。

以上程序是直接固定好了两个数字来进行除法运算，现在通过初始化参数来进行除法计算。

**范例** 接收参数进行计算：

	public class TestDemo {
		public static void main(String[] args) {
			System.out.println("【1】数学计算开始前");
			try {
				int x = Integer.parseInt(args[0]);
				int y = Integer.parseInt(args[1]);
				System.out.println("【2】数学计算: " + (x/y));
			} catch (ArithmeticException e) {
				e.printStackTrace();
			}finally {
				System.out.println("【FINALLY】 不管是否有异常都一定要执行此语句。");
			}
			System.out.println("【3】数学计算结束后");
		}
	}

**console：**

【1】数学计算开始前
【2】数学计算: 5
【FINALLY】 不管是否有异常都一定要执行此语句。
【3】数学计算结束后

args[0] = 10， args[1] = 2；

但是这个时候有可能会存在有如下的问题：

- 用户执行的时候并没有输入参数：

		Exception in thread "main" java.lang.ArrayIndexOutOfBoundsException: 0
			at bznoc171118.TestDemo.main(TestDemo.java:9)

- 用户执行的时候输入的时候不是数字：a，b

		java.lang.NumberFormatException: For input string: "a"

- 被除数为0：10 0

		java.lang.ArithmeticException: / by zero
			at bznoc171118.TestDemo.main(TestDemo.java:11)	
通过以上代码发现，原来在进行catch捕获异常的时候，如果没有捕获指定的异常，那么程序依然无法进行处理，所以现在最直白的解决方案就使用多个catch：

问题是如果真这么写代码，这么测试，不使用异常处理也一样，因为完全可以使用if-else进行判断，如果想要更好的处理异常，那么必须清楚异常处理流程。以上只是try...catch语法演示。




## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course90)
