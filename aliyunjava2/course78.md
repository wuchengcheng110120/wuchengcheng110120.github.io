## [上一页](course77)

## 包装类（包装类简介）

接触了Object类，发现Object能够接收所有的引用数据类型，于是这里面又出现了新的问题，数据类型可以分为基本类型和引用类型两类，那么基本数据类型该如何处理呢？

所谓的包装类指的就是将基本数据类型封装在一个类中，就好比如下的代码：

**范例**  

	class MyInt{
		private int num;
		public MyInt(int num) {
			this.num = num;
		}
		public int intValue() {
			return this.num;
		}
	}

这个时候的MyInt实际上就是一个int数据类型的包装类，利用MyInt可以实现基本数据类型变为对象的一个需求；

**范例** MyInt的使用：

	public class TestDemo {
		public static void main(String[] args) {
			//子类对象自动变为Object的父类对象
			Object obj = new MyInt(10);
			MyInt temp = (MyInt)obj;//取出内容需要向下转型
			System.out.println(temp.intValue()*2);//取出基本数据类型的操作
		}
	}

**console：**

	20

结论：将基本数据类型包装成一个类对象的本质就在于方便的使用Object进行接收处理。那么Java中有8种数据类型，如果每种类型都按以上的方式编写，那么会存在有如下问题：

- 发现所有的开发中代码会重复；

- 在进行数学计算的时候必须利用明确的方法将包装类中包装的基本数据取出后才可以进行。

所以Java为了方便用户开发，专门提供包装类的使用，包装类有两种类型：

- 对象型（Object的直接子类）：Boolean、Character（char）；

- 数值型	（Number的直接子类）： Byte、 Double、Short 、Long 、 Integer（int），Float；

**说明** 关于Number类

- Number类的定义：public abstract class Number extends Object implements Serializable

- 在Number类里面实际上定义有六个重要的方法：byteValue()、doubleValue()、floatValue()、intValue()、longValue()、shortValue()。




## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course79)
