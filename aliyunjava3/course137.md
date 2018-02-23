## [上一页](course136)
##  【第18个代码模型】 Set集合接口（重复元素判断）

在使用TreeSet进行数据保存的时候，重复元素的判断依靠的是Comparable接口完成的。但是这并不是所有Set接口判断重复元素的方式，因为如果使用的是HashSet子类，由于其跟Comparable没有任何关系，所以他判断重复元素的方式依靠的是Object类中的两个方法：

- hash码： public int hashCode()

- 对象比较： public boolean equals(Object obj)

在Java中进行对象比较的操作需要有两步：第一步要通过一个对象的唯一编码找到对象的信息，当编码匹配之后再调用equals()方法进行内容的比较。

	package cn.mldn.demo;
	
	import java.util.HashSet;
	import java.util.Set;
	
	class Person implements Comparable<Person>{
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
		public int hashCode() {
			final int prime = 31;
			int result = 1;
			result = prime * result + ((age == null) ? 0 : age.hashCode());
			result = prime * result + ((name == null) ? 0 : name.hashCode());
			return result;
		}
		@Override
		public boolean equals(Object obj) {
			if (this == obj)
				return true;
			if (obj == null)
				return false;
			if (getClass() != obj.getClass())
				return false;
			Person other = (Person) obj;
			if (age == null) {
				if (other.age != null)
					return false;
			} else if (!age.equals(other.age))
				return false;
			if (name == null) {
				if (other.name != null)
					return false;
			} else if (!name.equals(other.name))
				return false;
			return true;
		}
		@Override
		public String toString() {
			return "Person [name=" + name + ", age=" + age + "]" + "\n";
		}
		@Override
		public int compareTo(Person o) {
			if (this.age > o.age) {
				return 1;
			}else if (this.age < o.age) {
				return -1;
			}else {
				return this.name.compareTo(o.name);
			}
		}
	}
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			Set<Person> set = new HashSet<Person>();
			set.add(new Person("张三", 20));
			set.add(new Person("张三", 20)); //重复数据
			set.add(new Person("李四", 20)); //年龄重复
			set.add(new Person("王五", 19));
			System.out.println(set);
		} 	
	}
**console：**

	[Person [name=李四, age=20]
	, Person [name=王五, age=19]
	, Person [name=张三, age=20]
	]

如果想要标识出对象的唯一性，一定需要hashCode()、equals()两个方法共同作用。

面试题：如果两个对象的hashCode相同、equals不同，结果是什么？

不能消除重复

如果两个对象的hashCode不同、equals相同，结果是什么？

不能消除重复

对象判断必须两个都相同才能够实现消除重复元素

![](http://ww2.sinaimg.cn/large/0060lm7Tly1foq6fm9fw0j30vd0hcahz.jpg)

在很多时候使用Set集合的核心目的不是让其进行排序，而是让其进行重复元素的过滤。那么使用TreeSet就没有太大意义了，但是重复元素又需要依靠hashCode()、equals()两个方法，所以如果不是必须的时候，在使用Set接口的时候尽量用系统提供的类实现。例如： String、Integer。

原则：

保存自定义类对象一定用List接口；

保存系统类信息的时候一定使用Set接口。



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course138)
