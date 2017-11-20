## [上一页](course3)


### 2.3 类与对象（对象的内存分析） ###

如果想对对象进行产生分析，那么就必须清楚引用类型。

引用类型指的是内存空间的操作。所谓的引用类型就是获得储存空间。

而对于现在的内存，主要要会使用两块内存空间：

- 堆内存空间：保存真正的数据,堆内存保存的是对象的属性信息；
- 栈内存空间：保存的堆内存的地址，堆内存的操作权，如果想要简化理解，可以理解为保存的是对象名称；

		public class TestDemo {

			public static void main(String[] args) {
				// TODO Auto-generated method stub
				//类名称 对象名称 = new 类名称（）；
				Person person = new Person();
				
				person.info();//调用类中的方法
						
			}
		}

**console**：

	name = null、age = 0 

string初始化为null，int初始化为0

所以按照之前的程序，那么现在就给出如下的内存参考图：
![](https://i.imgur.com/OFOD6vQ.png)

但是对于对象的产生实际上要知道一共会有两种格式，现在使用的是声明并实例化对象的格式，那么也可以分步的方式完成。

	public class TestDemo {
		
		public static void main(String[] args) {
				
			Person person = null;
			person = new Person();
			person.info();//调用类中的方法
						
		}
	}

内存参考图：

![](https://i.imgur.com/wmFqEBh.png)

但是千万要记住一点，对象（所有的引用数据类型），必须在其开辟空间之后才可以使用。

如果使用了未开辟内存空间的引用数据类型，则将出现NullPointerException：

	public class TestDemo {
		
		public static void main(String[] args) {
			Person person = null;
			person.info();//调用类中的方法
						
		}		
	}


这个时候只声明了对象，而没有为其开辟堆内存空间，而本程序在编译的时候不会产生任何的语法错误，在执行的时候会出现如下的错误提示：

	Exception in thread "main" java.lang.NullPointerException
	at bznoc171118.TestDemo.main(TestDemo.java:20)

“NullPointerException”是在整个开发人生中陪伴你到最后的的异常，只有引用数据类型（数组、类、接口）才会出现此类异常，以后出现此类错误，根据出现错误的位置查看是否实例化。




## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course5)
