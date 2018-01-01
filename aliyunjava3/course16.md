## [上一页](course15)
## 枚举（枚举应用）

枚举最大的特点是有指定的几个对象可以使用。做一个最简单的应用，定义一个表示性别的枚举类，很明显只能有两个对象。所以现在的实现如下：

**范例** 枚举应用：

	package cn.mldn.demo;
	
	class Person{
		private String name;
		private int age;
		private Sex sex;
		public Person(String name, int age, Sex sex) {
			this.name = name;
			this.age = age;
			this.sex =sex;
		}
		@Override
		public String toString() {
			return "Person [name=" + name + ", age=" + age + ", sex=" + sex + "]";
		}
	}
	
	enum Sex{
		MALE("男"),FAMALE("女");
		private String title;
		private Sex(String title) {
			this.title =title;
		}
		public String toString() {
			return this.title;
		}
	}
	
	public class TestDemo {
		public static void main(String[] args) {
			Person per = new Person("张三", 20, Sex.MALE);
			System.out.println(per);
		}
	}
**console：**

	Person [name=张三, age=20, sex=男]

另外需要注意的是枚举本身还支持switch判断，也就是说switch按照时间进度来讲，最初只支持int和char，JDK 1.5的时候支持了枚举，到JDK1.7的时候支持了String。

	package cn.mldn.demo;
	
	enum Sex{
		MALE,FAMALE;
	}
	
	public class TestDemo {
		public static void main(String[] args) {
			switch (Sex.MALE) {
				case MALE:
					System.out.println("是男人");
					break;
				case FAMALE:System.out.println("是女人");
					break;
				default:
					break;
			}
		}
	}

好像不使用枚举所有的代码也可以写，所以对于枚举的使用根据个人习惯。


## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course17)
