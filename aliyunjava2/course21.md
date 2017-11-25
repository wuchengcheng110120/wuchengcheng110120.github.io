## [上一页](course20)

## 7.2 String类的基本特点（字符串比较）

如果有两个int型变量判断其是否相等，可以用==来判断

**范例** 观察基本数据类型比较：

	public class StringDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			int x =10;
			int y =10;
			System.out.println(x==y);
		}
	}

**console：**

	true

那么如果说在String类的对象上使用了“==”呢？

**范例** String类型比较使用"=="：

	public class StringDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			String str1 = "hello";
			String str2 = new String("hello");
			System.out.println(str1 == str2);
		}
	}

**console:**

	false

现在两个字符串的内容是相同的，而是用了“==”比较之后内容是不同的，于是想要得出结论，需要进行内存分析。

![](https://i.imgur.com/B4SkpZF.png)

“==”本身是进行数值比较的，而现在如果用在了对象之中，进行比较的就是两个内存地址的数值，所以属于地址数值比较，而并没有比较对象的内容，所以不能使用。

想要进行内容比较，则必须采用String类中所提供的一个方法（暂时变形）:

- 内容比较：public boolean equals(String str);

	    //String类中equals（）方法
		public boolean equals(Object anObject) {
	        if (this == anObject) {
	            return true;
	        }
	        if (anObject instanceof String) {
	            String anotherString = (String)anObject;
	            int n = value.length;
	            if (n == anotherString.value.length) {
	                char v1[] = value;
	                char v2[] = anotherString.value;
	                int i = 0;
	                while (n-- != 0) {
	                    if (v1[i] != v2[i])
	                        return false;
	                    i++;
	                }
	                return true;
	            }
	        }
	        return false;
	    }

**范例** 进行字符串对象内容比较：

	public class StringDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			String str1 = "hello";
			String str2 = new String("hello");
			System.out.println(str1.equals(str2));
		}
	}

**console：**

	true

最简单的面试题：请解释String类中“==”和“equals（）”的区别

- “==”：进行的是数值比较，比较的是两个字符串对象的内存地址数值；

- “equals（）”：可以进行字符串内容的比较；



>  PS：个人认为是String类是引用数据类型，不能用“==”来比较内容

![](https://i.imgur.com/aXJs0Vo.png)

特点：

一、从概念方面来说

基本数据类型:变量名指向具体的数值
引用数据类型:变量名指向存数据对象的内存地址,即变量名指向hash值

二、从内存构建方面来说

基本数据类型:变量在声明之后java就会立刻分配给他内存空间

引用数据类型:它以特殊的方式(类似C指针)指向对象实体（具体的值），这类变量声明时不会分配内存，只是存储了一个内存地址。

三、从使用方面来说

基本数据类型:使用时需要赋具体值,判断时使用“==”号

引用数据类型:使用时可以赋null,判断时使用equals（）方法

## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course22)
