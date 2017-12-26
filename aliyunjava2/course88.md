## [上一页](course87)

## 【第04个代码模型】异常的捕获与处理（观察异常带来的问题）

几乎所有的代码中都可能产生异常，所以为了保证程序出现异常之后能够正常执行完毕，就需要进行异常处理。

异常是导致程序中断执行的一种指令流，但是程序之中如果出现异常并且没有合理处理的话，就会导致程序终止执行。

**范例** 观察没有异常产生的程序：

	public class TestDemo {
		public static void main(String[] args) {
			System.out.println("【1】数学计算开始前");
			System.out.println("【2】数学计算: " + (10/2));
			System.out.println("【3】数学计算结束后");
		}
	}
**console：**

	【1】数学计算开始前
	【2】数学计算: 5
	【3】数学计算结束后

如果没有任何的异常产生，那么程序可以正常的执行完毕。

**范例** 观察产生异常：

	public class TestDemo {
		public static void main(String[] args) {
			System.out.println("【1】数学计算开始前");
			System.out.println("【2】数学计算: " + (10/0));
			System.out.println("【3】数学计算结束后");
		}
	}
**console：**

	【1】数学计算开始前
	Exception in thread "main" java.lang.ArithmeticException: / by zero
		at bznoc171118.TestDemo.main(TestDemo.java:8)

现在程序之中产生了异常，但是在异常语句之前的代码依然可以正常执行完毕，而异常产生之后程序将直接结束，为了保证在程序出现异常后还可以继续向下执行，就需要进行异常处理。


## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course89)
