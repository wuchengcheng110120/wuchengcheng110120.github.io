## [上一页](course89)

## 【第04个代码模型】异常的捕获与处理（throws关键字）

在方法定义的时候，如果要告诉调用者本方法可能产生哪些异常，你就可以使用throws进行声明，如果该方法出现问题后不希望进行处理，就使用throws抛出。

**范例** 使用throws定义方法：

class MyMath{
	//此处明确告诉用户该方法会产生异常
	public static int div(int x, int y) throws Exception{
		return x/y;
	}
}

public class TestDemo {
	public static void main(String[] args) {
		try{
			System.out.println(MyMath.div(10, 0));
		}catch (Exception e) {
			e.printStackTrace();
		}
	}
}

**console：**

	java.lang.ArithmeticException: / by zero
		at bznoc171118.MyMath.div(TestDemo.java:6)
		at bznoc171118.TestDemo.main(TestDemo.java:13)

如果你现在调用了throws声明的方法，那么在调用时就必须明确的使用try...catch进行异常捕获，因为该方法有可能产生异常，所以必须按照异常的方式来进行处理。

主方法本身也属于一个方法，所以主方法上也可以使用throws进行异常的抛出，这个时候如果产生了异常就会交给JVM来进行处理。

	class MyMath{
		//此处明确告诉用户该方法会产生异常
		public static int div(int x, int y) throws Exception{
			return x/y;
		}
	}
	public class TestDemo {
		public static void main(String[] args) throws Exception{
				System.out.println(MyMath.div(10, 5));
		}
	}

**console：**

	2

在以后的代码中一定要斟酌好可能产生的异常，因为面对未知的程序类，如果要进行异常的处理就必须要知道存在多少种异常。



## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course91)
