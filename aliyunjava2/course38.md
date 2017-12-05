## [上一页](course37)

## 【第02个代码模型】综合案例：对象比较

比较两个对象是否相等，应该比较的是对象的完整信息，而对象的完整信息就是对象的属性，所以所谓的对象比较指的就是两个对象的属性进行比较。

**范例：** 对象比较的实现形式一:

	class Person {
		private String name;
		private int age;
		public Person(String name, int age) {
			this.name = name;
			this.age = age;
		}
		public String getName() {
			return this.name;
		}
		
		public int getAge() {
			return this.age;
		}	
	}
	
	public class TestDemo {
		public static void main(String[] args) {
			Person perA = new Person("张三", 20);
			Person perB = new Person("张三", 20);
			System.out.println(perA == perB);
			//需要对象拥有的属性信息进行完整比对
			if (perA.getName().equals(perB.getName()) && perA.getAge() == perB.getAge()) {
				System.out.println("两个对象相等！ ");
			}else {
				System.out.println("两个对象不等！ ");
			}			
		}	
	}

**console: **

	false
	两个对象相等！ 

虽然这个时候已经实现了对象的比较，但是这种操作一定不可能在实际工作中出现，因为客户端（主方法、调用处需要涉及的逻辑过多），对象比较的操作应该是一个类本身所具备的功能，而不应该变为外部操作。
对象比较方法暂时命名为compare（）；

**范例：** 对象比较的实现形式二:

	class Person {
		private String name;
		private int age;
		public Person(String name, int age) {
			this.name = name;
			this.age = age;
		}
		public void setName(String name) {
			this.name = name;
		}
		public void setAge(int age) {
			this.age = age;
		}
		public String getName() {
			return this.name;
		}
		public int getAge() {
			return this.age;
		}	
		//这个时候会有两个对象出现，this当前对象，传入对象
		public boolean compare(Person per) {
			//此时per对象已经在类的内部了，所以不受封装局限
			//可以直接利用“对象.属性”进行访问（固定概念）
			if (per == this) {//传入对象与当前对象地址相同
				return true;
			}
			if (per == null) {
				return false;
			}
			if(this.name.equals(per.name) && this.age == per.age ) {
				return true;
			}
			return false;
		}
	}

	public class TestDemo {
		public static void main(String[] args) {
			Person perA = new Person("张三", 20);
			Person perB = new Person("张三", 20);
			//需要对象拥有的属性信息进行完整比对
			if (perA.compare(null)) {
				System.out.println("两个对象相等！ ");
			}else {
				System.out.println("两个对象不等！ ");
			}					
		}	
	}

**console：**

	两个对象不相等！ 

对象比较是一个类本身所具备的功能，对象比较最核心的问题：比较地址、判断是否为空、比较各个属性。

## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course39)
