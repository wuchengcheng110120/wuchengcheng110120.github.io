## [上一页](course91)
##  【第13个代码模型】对象序列化（序列化基本概念）

所有的项目开发一定都有序列化的概念存在，所谓的对象序列化指的是将在内存中保存的对象变为二进制数据流的形式进行传输，或者是将其保存在文本中。

并不意味着所有类的对象都可以被序列化，严格来讲，需要被序列化的类往往需要被传输使用，同时这个类必须实现java.io.Serializable接口。但是这个接口并没有任何的方法定义，只是一个标示接口。

**范例** 定义一个可以被序列化的对象类；

	import java.io.Serializable;
	
	@SuppressWarnings("serial")
	class Person implements Serializable{
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
	}

序列化对象时所需要保存的就是对象中的属性，所以默认情况下对象的属性将被转为二进制数据流存在。




## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course93)
