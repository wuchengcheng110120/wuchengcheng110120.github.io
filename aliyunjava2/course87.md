## [上一页](course86)

## 单例设计模式（多例设计模式）

多例对象的类在生活中也经常出现，例如：要求描述一周时间数的类，只能有七个对象；描述性别类的对象，只能有两个对象，这些都属于多例设计模式；

所谓的多例只是比单例追加了更多个内部实例化对象的产生而已。

**范例** 现在定义一个表示性别的多例类：

	class Sex{
		public static final int MALE_CMD = 1;
		public static final int FAMALE_CMD = 2;
		private static final Sex MALE = new Sex("男");
		private static final Sex FAMALE = new Sex("女");
		private String title;
		private Sex(String title) {//构造方法必须私有化
			this.title =title;
		}
		public static Sex getInstance(int ch) {
			switch (ch) {
			case MALE_CMD:
				return MALE;
			case FAMALE_CMD:
				return FAMALE;
			default:
				return null;
			}
		}
		public String toString() {
			return this.title;
		}
	}
	public class TestSingleton{
		public static void main (String args[]) {
			Sex a = Sex.getInstance(Sex.MALE_CMD);
			System.out.println(a);
		}
	}

不管单例还是多例都具有共同特点：

- 构造方法私有化；

- 类内部一定会提供有一个static方法用于取得类的实例化对象；

单例和多例的代码编写的几率并不会很高，但是对于代码结构必须清楚。多例设计模式先理解概念，该概念已经被枚举所取代了。


## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course88)
