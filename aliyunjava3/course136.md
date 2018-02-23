## [上一页](course135)
##  【第18个代码模型】 Set集合接口（集合排序说明）

既然TreeSet子类可以进行排序，下面自己编写一个类希望可以通过TreeSet来实现数据的排列处理。此时的排序是针对对象数组进行的排序处理，而如果要进行对象数组的排序，而如果要进行对象数组的排序，之前就已经说明了，对象所在的类一定要实现Ccomparable接口，而且要覆写compareTo()方法，因为只有通过此方法才能知道大小关系。

但是需要提醒的是，如果使用Comparable接口进行大小关系匹配的时候，有一个坑存在，所有的属性必须全部进行比较操作。

**范例** 使用TreeSet排序：

	package cn.mldn.demo;
	
	import java.util.Set;
	import java.util.TreeSet;
	
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
			Set<Person> set = new TreeSet<Person>();
			set.add(new Person("张三", 20));
			set.add(new Person("张三", 20)); //重复数据
			set.add(new Person("李四", 20)); //年龄重复
			set.add(new Person("王五", 19));
			System.out.println(set);
		} 	
	}
**console：**

	[Person [name=王五, age=19]
	, Person [name=张三, age=20]
	, Person [name=李四, age=20]
	]

因为在实际的开发之中TreeSet的使用过于麻烦了，在项目开发中简单Java类是根据数据表设计的来的，如果一张表的字段暴多，此类的compareTo()会非常复杂。

![](http://ww1.sinaimg.cn/large/0060lm7Tly1foq5af0sltj30vf0hh7bl.jpg)



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course137)
