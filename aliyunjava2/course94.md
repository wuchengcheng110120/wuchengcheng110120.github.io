## [上一页](course93)

## 【第04个代码模型】异常的捕获与处理（断言）

断言（assert）是从JDK1.4引入的概念，所谓断言的概念指的是当程序执行到某些语句之后其数据的内容一定是约定的内容。

**范例** 观察一下断言：

	public class TestDemo {
		public static void main(String[] args) {
				int num =10;
				//中间经过很多步预计num内容变为300
				assert num == 300 : "错误： num的内容不是300";
				System.out.println(num);
		}
	}
**console：**
	
	10

如果要让断言起作用，则必须使用一个-ea的参数；

实际上断言的引入作用不大，Java之所以要引入主要是为了与C++相同，所以开发中不提倡使用断言。



## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course95)
