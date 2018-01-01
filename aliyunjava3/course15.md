## [上一页](course14)
## 枚举（枚举中定义其他结构）

虽然枚举等同于多例设计，多例是在类中产生的，所以该类中可以定义更多的属性或者是方法。
于是只依靠以上的概念只能够说产生了若干个对象，并没有方法去定义更多的结果，所以在枚举设计的时候
考虑到了这些因素，提出了更强大的枚举设计方案：可以在枚举里面定义属性、方法、或者实现接口。

**范例** 在枚举中定义更多的结构：

	package cn.mldn.demo;
	
	enum Color {
		RED("红色"),GREEN("绿色"),BLUE("蓝色");//如果定义有很多内容，枚举对象必须写在第一行
		private String title;
		private Color(String title) {//枚举就是多例设计，构造方法绝对不可以使用public
			this.title = title;
		}
		public String toString() {//覆写Object类中的toString（）方法
			return this.title;
		}
	}
	
	public class TestDemo {
		public static void main(String[] args) {
			for(Color temp: Color.values()) {
				System.out.println(temp);
			}
		}
	}
**console：**

	红色
	绿色
	蓝色

枚举还可以实现接口，这样枚举中的每一个对象实际上就都变成了接口对象。

**范例**  枚举实现接口：

	package cn.mldn.demo;
	
	interface IColor{
		public String getColor();
	}
	
	enum Color implements IColor{
		RED("红色"),GREEN("绿色"),BLUE("蓝色");//如果定义有很多内容，枚举对象必须写在第一行
		private String title;
		private Color(String title) {//枚举就是多例设计，构造方法绝对不可以使用public
			this.title = title;
		}
		public String toString() {//覆写Object类中的toString（）方法
			return this.title;
		}
		@Override
		public String getColor() {
			return this.title;
		}
	}
	
	public class TestDemo {
		public static void main(String[] args) {
			IColor ic = Color.RED;
			System.out.println(ic.getColor());
		}
	}

**console：**

	红色

这些只能够算枚举的扩展特点，其他语言中的枚举没有这么高级的特性。


## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course16)
