## [上一页](course23)

## 7.5 String类的基本特点（字符串常量不可变更）

字符串一旦定义不可改变，字符串的底层实现都是字符数组，数组的最大缺陷就是不能改变长度固定，所以在定义字符串产量的时候，字符串常量是不能改变的。

**范例** 观察如下代码：

	public class StringDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub		
			String str = "hello ";
			str = str + "world ";
			str += "!!!";
			System.out.println(str);
		}
	}

**console：**

	hello world !!!

以上字符串的变更是对象字符串的变更，而并不是字符串的内容变更。

![](https://i.imgur.com/iwiKmnu.png)

可以发现字符串没有发生变化，字符串对象的引用在发生改变，并且形成大量垃圾，正是因为String的这个特点，所以以下的代码不应该在开发中出现。

**范例** 观察如下代码：

	public class StringDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub		
			String str = "hello ";
			for(int x = 0; x<10; x++) {
				str +=x;
			}
			System.out.println(str);
		}
	}


**console：**

	hello 0123456789

以上操作产生大量垃圾，字符串常量定义以后不建议修改。

> 总结

> - 字符串的使用采用直接赋值的模式完成；

> - 字符串的比较使用equals（）方法实现；

> - 字符串不要多次改变

## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course25)
