## [上一页](course75)

## Object类（对象比较）

String类内容的比较使用的是equals（）方法，实际上这个equals（）方法就是String类覆写的Object类的方法。

- String类中的equals:

	public boolean equals(Object anObject)

以后再编写对象比较的处理，不要再使用之前的compare（）了，统一更换为equals。

**范例** 实现对象比较：

	class Person{
		private String name;
		private int age;
		public Person(String name, int age) {
			this.name = name;
			this.age = age;
		}
		public boolean equals(Object anObject) {
			if (anObject == null) {
				return false;
			}
			if (this == anObject) {
				return true;
			}
			if (!(anObject instanceof Person)) {
				return false;
			}
			//必须将Object类型变为Person类型后才可以调用name和age属性
			Person per = (Person) anObject;
			return this.name.equals(per.name) && this.age == per.age;
		}
		public String toString() {//覆写Object类中的方法
			return "姓名： "  + this.name +  ", 年龄： "   +  this.age ;
		}
	}
	public class TestDemo {
		public static void main(String[] args) {
			Person per1 = new Person("张三", 20);
			Person per2 = new Person("张三", 20);
			System.out.println(per1.equals("hello"));
			System.out.println(per1.equals(per2));
		}
	}

**console：**

	false
	true

开发过程中极少出现对象比较。

需要注意，很多人在写对象比较的时候会使用如下的形式：

- public boolean equals(Person anObject)

因为父类中的equals方法用的是Object，所以严格来讲以上的方法不是覆写了，叫重载；




## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course77)
