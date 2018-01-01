## [上一页](course17)
## Annotation（准确覆写）

方法覆写：发生在继承关系之中，子类定义了与父类的方法名称相同、参数类型及个数、返回值类型相同方法的时候称为方法的覆写，被覆写的方法不能够拥有比父类更为严格的访问控制权限。

	package cn.mldn.demo;
	
	class Person{
		//现在希望进行toString的覆写，由于输入错误导致方法覆写错误
		public String tostring() {//现在希望进行toString（）方法的覆写
			return "是一个人";
		}
	}
	
	
	public class TestDemo {
		public static void main(String[] args) {
			System.out.println(new Person());
		}
	}

这个时候不是覆写，而是属于自己定义了一个扩展的方法，最为重要的是，这个问题程序编译的时候不会显示出来，所以现在为了覆写方法的严格，可以使用一个注解（@Override）来检测：如果该方法确定成功覆写了，则不会有语法错误，如果没有成功的覆写则认为是语法错误。

	语法错误：The method tostring() of type Person must override or implement a supertype method

	package cn.mldn.demo;
	
	class Person{
		//现在希望进行toString的覆写，由于输入错误导致方法覆写错误
		@Override  //追加了此注解后将明确的表示该方法是一个覆写的方法，如果覆写错误则会出现语法错误
		public String tostring() {//现在希望进行toString（）方法的覆写
			return "是一个人";
		}
	}
	public class TestDemo {
		public static void main(String[] args) {
			System.out.println(new Person());
		}
	}

当覆写方法正确时不会有任何语法错误，当覆写错误时会有语法错误提示

	class Person{
		//现在希望进行toString的覆写，由于输入错误导致方法覆写错误
		@Override  //追加了此注解后将明确的表示该方法是一个覆写的方法，如果覆写错误则会出现语法错误
		public String toString() {//现在希望进行toString（）方法的覆写
			return "是一个人";
		}
	}

在Eclipse里只要是你覆写的方法都会有该注解自动生成。


## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course19)
