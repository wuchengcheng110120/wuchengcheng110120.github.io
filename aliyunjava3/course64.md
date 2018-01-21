## [上一页](course63)
## 【第09个代码模型】正则表达式（正则问题引出）

在开发过程中正则一定会使用，但是正则的使用难易也是看实际的开发情况，如果只是项目功能的实现，对于正则不需要过多深入的理解，如果需要做特别复杂的符号匹配操作，那么就需要用正则表达式更深入的内容来完成。

现在要求判断某一个字符串是否全部由数字组成。最初的实现采用的是拆分为字符数组，而后依次判断每一个字符的方式实现的

	package cn.mldn.demo;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			System.out.println(isNumber("abc"));
			System.out.println(isNumber("12c"));
			System.out.println(isNumber("123"));
		}
		public static boolean isNumber(String str) {
			char[] data = str.toCharArray();
			for (int i = 0; i < data.length; i++) {
				if (data[i] < '0' || data[i] > '9') {
					return false;
				}
			}
			return true;
		}
	}

**console：**

	false
	false
	true

现在一个小小的验证都要编写8行代码，那么如果更加复杂的验证呢？所以这种传统的验证实际上就非常的不方便，在实际的开发之中也不可能使用，所以这个时候我们可以采用正则的方式来处理。

**范例** 用正则来进行字符串的验证：

	package cn.mldn.demo;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			System.out.println("abc".matches("\\d+"));
			System.out.println("12c".matches("\\d+"));
			System.out.println("123".matches("\\d+"));
		}
	}

**console：**

	false
	false
	true

在程序之中所见的"\\d+"就属于正则表达式范畴，而有了正则表达式针对于字符串的验证就会非常简单，实际开发过程中使用最多的也是对于字符串数据的验证。

正则表达式最早是从Linux下发展的（Perl），在JDK1.4以前正则并没有引入到java的开发包之中，所以当时要想使用正则就必须进行其它开发包的配置，而从JDK1.4开始正则引入到了Java的项目里面，并且提供了专门的新的开发包：java.util.regex。

想要理解正则建议学习离散数学。



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course65)
