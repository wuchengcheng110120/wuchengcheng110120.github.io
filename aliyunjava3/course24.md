## [上一页](course23)
## 内建函数式接口

Lamdba语法实际上简化为了方法引用，但是Lamdba核心在于函数式接口，而函数式接口的核心在于只有一个方法，实际上在函数式编程里面只需要有四类接口（java.util.function）：

- 功能型函数式接口：public interface Function<T,R>{public R apply(T t)}

- 供给型函数式接口：public interface Supplier<T>{public T get()}

- 消费型函数式接口：public interface Consumer<T>{public void accept(T t)}

- 断言型函数式接口：public interface Predicate<T>{public boolean test(T t)}

**范例** 使用功能型函数式接口（String.valueOf（））：

	package cn.mldn.demo;
	
	import java.util.function.Function;
	
	public class TestDemo {
		public static void main(String[] args) {
			Function<Integer, String> fun = String :: valueOf;
			System.out.println(fun.apply(1000));
		}
	}

功能型指的是你输入一个数据，而后将数据处理之后再输出实际上所有的函数式接口都会有一些小小的扩展，如果现在确定操作的数据是int，则可以使用intFunction接口。

**范例** 扩展的Function接口：

	package cn.mldn.demo;
	
	import java.util.function.IntFunction;
	
	public class TestDemo {
		public static void main(String[] args) {
			IntFunction<String> fun = String :: valueOf;
			System.out.println(fun.apply(1000));
		}
	}

**范例** 消费型函数式接口（System.out.println()）:

	package cn.mldn.demo;
	
	import java.util.function.Consumer;
	
	public class TestDemo {
		public static void main(String[] args) {
			Consumer<String> cons = System.out :: println;
			cons.accept("Hello World !");
		}
	}

**范例** 供给型函数式接口（“hello”.toUpperCase（））：

	package cn.mldn.demo;
	
	import java.util.function.Supplier;
	
	public class TestDemo {
		public static void main(String[] args) {
			Supplier<String> sup = "hello" :: toUpperCase;
			System.out.println(sup.get());
		}
	}

**范例** 断言型函数式接口（isEmpty（））：

	package cn.mldn.demo;
	
	import java.util.function.Predicate;
	
	public class TestDemo {
		public static void main(String[] args) {
			Predicate<String> pre = "##hello" :: startsWith;
			System.out.println(pre.test("##"));
		}
	}
如果以后要进行复杂的Lamdba运算，就需要这类函数式接口进行操作。

## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course25)
