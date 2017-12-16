## [上一页](course61)

## final关键字

在java中final被称为终结器，可以使用final来定义类、方法、常量。

1、 使用final定义的类不允许拥有子类；

	final class  A {}//这个时候A类不允许有子类
	class B extends A{//语法出现错误
	}

	public final class String
	extends Object
	implements Serializable, Comparable<String>, CharSequence{}

2、 使用final定义的方法不允许被子类覆写；

	class  A {
		public final void fun() {	
		}
	}
	class B extends A{
		public void fun() {//语法出现错误
		}
	}

3、 使用final定义的变量就成为了常量，常量必须在声明时赋值，并且不允许被修改；

	class  A {
		public final int LEVEL_A = 100;
		public final void fun() {
			LEVEL_A = 20;//语法错误
		}
	}
在开发之中如果要定义常量，往往会使用public static final 来定义全局常量。

	public static final int LEVEL_A = 100;

而且常量的标识符必须全部采用大写字母形式出现；

## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course63)
