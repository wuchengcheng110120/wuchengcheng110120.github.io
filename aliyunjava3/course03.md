
## [上一页](course02)
## Eclipse开发工具（debug调试）

简单程序类：

	package cn.mldn.util;
	
	public class MyMath {
		public static int add(int x, int y) {
			int temp = 0;
			temp = x + y;
			return temp;
		}
	}
	
随后在另外一个测试类中要进行代码的调试处理。

**范例** 定义测试类：

	package cn.mldn.demo;	
	import cn.mldn.util.MyMath;	
	public class TestMath {
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			int result = MyMath.add(10, 20);
			System.out.println("加法结果： " + result);
		}
	}

双击行数名设置断点，随后右键-》Debug As ；

询问是否切换至调试视图中，选择Yes，进入调试视图；

如果要进行调试有以下几种形式：

- 单步跳入【F5】：进入到代码之中观察，进入代码内部；

- 单步跳过【F6】：不进入到代码之中观察，只观察代码的表面；

- 单步返回【F7】：后面的代码不再调试，返回到进入处；

- 恢复执行【F8】：程序直接正常执行完毕； 



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course04)
