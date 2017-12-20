## [上一页](course73)

## Object类（Object类简介）

Object是Java默认提供的一个类，可以这样说，Java里面除了Object类之外，所有的类都是存在有继承关系的。默认会继承Object父类，也就是说以下两种类的定义最终效果是完全相同的：

	class Message{
	}

	class Message extends Object{
	}

那么也就证明所有类的对象都可以使用Object进行接收；

	class Message extends Object{}
	class Person{}
	public class TestDemo {
		public static void main(String[] args) {
			fun(new Message());
			fun(new Person());
		}
		public static void fun(Object obj) {//所有的类对象都可以进行接收
			System.out.println(obj);
		}
	}

**console：**

	bznoc171118.Message@52e922
	bznoc171118.Person@25154f

所以在开发之中Object类是参数的最高统一类型。但是Object类本身也有一些定义过的方法。

 No. | 方法名 | 类型 | 描述
-|-|-|--|
01 | public Object() | 构造 | 无参构造是专门为子类提供服务的
02 | public String toString() | 普通 | 取得对象信息
03 | public boolean equals(Object obj) | 普通 | 对象的比较

对于整个Object类中的方法需要一点一点消化。




## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course75)
