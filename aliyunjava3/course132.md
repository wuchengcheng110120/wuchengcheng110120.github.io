## [上一页](course131)
##  【第18个代码模型】 List集合接口（List与简单Java类）

之前向List中添加String。

在实际的开发之中，集合里面保存最多的数据类型，就是简单Java类。所以下边针对简单Java类的集合操作做一个说明：

**范例** 向集合保存简单Java类对象：

	package cn.mldn.demo;
	
	import java.util.ArrayList;
	import java.util.Arrays;
	import java.util.Collection;
	import java.util.List;
	
	class Person {
		private String name;
		private Integer age;
		public Person(String name, Integer age) {
			this.name = name;
			this.age = age;
		}
		public String getName() {
			return name;
		}
	
		public void setName(String name) {
			this.name = name;
		}
	
		public Integer getAge() {
			return age;
		}
	
		public void setAge(Integer age) {
			this.age = age;
		}
		@Override
		public boolean equals(Object obj) {
			if (this == obj) {
				return true;
			}
			if (obj == null) {
				return false;
			}
			if (!(obj instanceof Person) ) {
				return false;
			}
			Person per = (Person)obj;  // 向下转型
			return this.name.equals(per.name) && this.age.equals(per.age);
		}
		@Override
		public String toString() {
			return "Person [name=" + name + ", age=" + age + "]";
		}
	}
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			List<Person> all = new ArrayList<Person>();
			all.add(new Person("张三", 10));
			all.add(new Person("李于", 11));
			all.add(new Person("挖宝", 12));
			// 对于集合中的remove()，contains()方法中必须有equals()的支持
			all.remove(new Person("李于", 11));
			System.out.println(all.contains(new Person("李于", 11)));
			for (int x = 0; x < all.size(); x++) {
				System.out.println(all.get(x));
			}
		} 	
	}
**console：**

	false
	Person [name=张三, age=10]
	Person [name=挖宝, age=12]

从理论上讲contains()和remove()需要equals()的支持，实际上很少有人这样做，也就是说简单java类中实现equals方法的几率在开发中出现的可能性是很低的。


## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course133)
