## [上一页](course48)
## 数字操作类（随机数）

java中使用java.util.Random类来实现随机数操作

public class Random
extends Object
implements Serializable

**范例** 产生随机整数：

	package cn.mldn.demo;
	
	import java.util.Random;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			Random rand = new Random();
			for (int i = 0; i < 10; i++) {
				System.out.println(rand.nextInt(100) + "、");
			}
		}
	}

在许多网站上的英文随机验证码可以通过此类模式完成


	package cn.mldn.demo;
	
	import java.util.Random;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			char data[] = new char[] {'a','b','c','d','e'};
			Random rand = new Random();
			for (int i = 0; i < 3; i++) {
				System.out.print(data[rand.nextInt(data.length)]);
			}
		}
	}

中文验证码可以通过写中文验证码库完成；



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course50)
