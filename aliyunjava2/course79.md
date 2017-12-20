## [上一页](course78)

## 包装类（装箱与拆箱）

在包装类与基本数据类型的处理中存在两类概念：

- 装箱： 将基本数据类型变为包装类对象；

	|-利用每个包装类提供的构造方法实现装箱处理

- 拆箱：将包装类中包装的基本数据类型取出；

	|-利用Number类中提供的一系列xxxxValue（）方法

**范例** 以int和Integer为例：

	public class TestDemo {
		public static void main(String[] args) {
			Integer num = new Integer(10);//装箱
			int x = num.intValue();//拆箱
			System.out.println(x*2);
		}
	}

**console：**

	20

**范例** 以double和Double为例：

	public class TestDemo {
		public static void main(String[] args) {
			Double num = new Double(20.1);//装箱
			double x = num.doubleValue();//拆箱
			System.out.println(x*2);
		}
	}
**console：**

	40.2

以上的操作采用的是手动的装箱和拆箱操作形式，而这种做法是在JDK1.5之前的做法，而从JDK1.5之后提供有自动装箱与自动拆箱的机制，更为重要的是，由于此类机制的存在，可以直接利用包装类的对象进行各种数学计算。

**范例** 自动装箱与拆箱处理：

	public class TestDemo {
		public static void main(String[] args) {
			Integer x = 10;//自动装箱
			//这个时候发现可以直接利用包装类对象操作
			System.out.println(++x * 2);
		}
	}
**console：**

	22

但这个时候依然存在有“==”和equals（）问题。

**范例** 观察问题：

	public class TestDemo {
		public static void main(String[] args) {
			Integer num1 = 10;//自动装箱
			Integer num2 = 10;//自动装箱
			System.out.println(num1 == num2);
			System.out.println(num1 == new Integer(10));
			System.out.println(num1.equals(new Integer(10)));
		}
	}

**console：**

	true
	false
	true

**选择 ：** 使用int还是Integer？

- 在接收数据的时候，使用的一定都是int，而保存数据的时候会使用Integer；

		public class TestDemo {
			public static void main(String[] args) {
				int x = 0;
				Integer y = null;
				System.out.println(x);
				System.err.println(y);
			}
		}

**console：**

		0
		null

- 以后编写的简单Java类不要再去使用基本数据类型，全部更换为包装类；


## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course80)
