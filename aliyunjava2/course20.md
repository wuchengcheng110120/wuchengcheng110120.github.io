## [上一页](course19)

## 7.1 String类的基本特点（String类两种实例化方式）

几乎所有的项目开发过程中都一定会存在有String类的使用，但是String本身的定义是有一些差别，以及在使用上是有一些注意事项的。

String可以直接采用赋值的形式进行处理，和基本数据类型是非常相似的。

**范例** 直接赋值实例化对象：

	public class StringDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			//str是一个对象
			String str = "hello";
			System.out.println(str);
		}
	}

**console：**

	hello

但是String本身毕竟是一个类。既然是类类中就一定会提供构造方法，而在String类里面恰好提供了以下的构造方法：

- 构造： 
	
		public String(String original) {
	        this.value = original.value;
	        this.hash = original.hash;
	    }

**范例** 使用关键字new进行对象实例化：

	public class StringDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			//该过程符合传统做法，有类之后通过关键字new进行对象实例化
			String str = new String("hello");
			System.out.println(str);
		}
	}
暂时不需要考虑这两者的区别以及使用，关键是需要清楚String类提供有两种实例化对象的模式。


## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course21)
