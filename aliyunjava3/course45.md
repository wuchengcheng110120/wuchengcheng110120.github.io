## [上一页](course44)
## 对象克隆

克隆就是一个对象复制的概念，不过这种概念一般使用比较少，因为很少有人会去复制已经存在的对象。Object类本身就支持对象克隆方法，可以发现：

protected Object clone()
                throws CloneNotSupportedException；

CloneNotSupportedException - 

if the object's class does not support the Cloneable interface. Subclasses that override the clone method can also throw this exception to indicate that an instance cannot be cloned.

如果对象类不支持Cloneable的接口，覆写clone方法的子类也会抛出异常声明实例不能被克隆；

需要被克隆的对象所在类一定要实现Cloneable的接口，而最关键的是该接口并没有任何的抽象方法，所以该接口只是一个标识接口，表示一种能力。

**范例** 对象克隆实现：

	package cn.mldn.demo;
	
	class Person implements Cloneable{
		private String name;
		private int age;
		public Person(String name, int age) {
			super();
			this.name = name;
			this.age = age;
		}
		public String getName() {
			return name;
		}
		public void setName(String name) {
			this.name = name;
		}
		public int getAge() {
			return age;
		}
		public void setAge(int age) {
			this.age = age;
		}
		@Override
		public String toString() {
			return "Person [name=" + name + ", age=" + age + "]";
		}
		@Override
		public Object clone() throws CloneNotSupportedException {
			return super.clone();//父类负责克隆
		}
	}
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			Person perA = new Person("张三",10);
			Person perB = (Person)perA.clone();
			perB.setAge(20);
			System.out.println(perA);
			System.out.println(perB);
			
		}
	}
**console：**

	Person [name=张三, age=10]
	Person [name=张三, age=20]

对象克隆的操作本身意义不大，关键是要清楚标识接口的作用，表示一个能力。


## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course46)
