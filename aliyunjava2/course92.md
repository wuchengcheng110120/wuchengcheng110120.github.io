## [上一页](course91)

## 【第04个代码模型】异常的捕获与处理（异常处理模式）

现在异常处理中的所有核心概念都掌握了：try、catch、finally、throws、throw。

现在要求编写一个方法------进行除法操作，但是对于此方法的要求如下：

- 在进行除法操作之前首先要打印一行语句；

- 如果在除法计算的过程之中出现有错误，则应该将异常返回给调用处；

- 不管最终是否有错误产生，都要求打印一行错误信息；

**范例** 观察程序的实现：

	class MyMath{
		//如果该方法不进行异常的处理，一定要使用throws抛出
		public static int div(int x, int y) throws Exception{
			int result = 0;
			System.out.println("【开始】 进行除法计算");
			try {
				result = x/y;//此处有异常后面不执行
			}catch (Exception e) {
				throw e;
			}finally {
			System.out.println("【结束】 除法计算完毕");
			}
			return result;
			
		}
	}
	public class TestDemo {
		public static void main(String[] args) {
				try {
					System.out.println(MyMath.div(10, 0));
				} catch (Exception e) {
					e.printStackTrace();
				}
		}
	}
**console：**

	【开始】 进行除法计算
	【结束】 除法计算完毕
	java.lang.ArithmeticException: / by zero
		at bznoc171118.MyMath.div(TestDemo.java:9)
		at bznoc171118.TestDemo.main(TestDemo.java:22)

可以进一步简化:直接使用try...finally

	class MyMath{
		//如果该方法不进行异常的处理，一定要使用throws抛出
		public static int div(int x, int y) throws Exception{
			int result = 0;
			System.out.println("【开始】 进行除法计算");
			try {
				result = x/y;//此处有异常后面不执行
			}finally {
			System.out.println("【结束】 除法计算完毕");
			}
			return result;
			
		}
	}
	public class TestDemo {
		public static void main(String[] args) {
				try {
					System.out.println(MyMath.div(10, 0));
				} catch (Exception e) {
					e.printStackTrace();
				}
		}
	}

对于此时的格式一定要吸收理解。



## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course93)

