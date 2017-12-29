## [上一页](course03)
## Eclipse开发工具（junit测试工具）


junit 是一种用例测试工具

**范例** 建立一个简单的程序类

	package cn.mldn.util;
	
	public class MyMath {
		public static int add(int x, int y) {
			int temp = 0;
			temp = x + y;
			return temp;
		}
	}

选中这个类要测试的类进行junit的测试创建，继续选择新建；

junit属于第三方的程序包，所以需要进行额外的jar文件的配置

**范例** 编写测试程序：

	package cn.mldn.test;
	import org.junit.jupiter.api.Test;	
	import cn.mldn.util.MyMath;
	import junit.framework.TestCase;
	
	class MyMathTest {
		@Test
		void testAdd() {
			TestCase.assertEquals(MyMath.add(10, 20), 30);
		}
	}

junit测试有两个结果：

		- GREEN BAR: 测试通过:
		- RED BAR: 测试失败；



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course05)
