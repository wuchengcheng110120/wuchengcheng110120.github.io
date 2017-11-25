## [上一页](course18)

## 6.11 对象数组

之前所定义的数组都属于基本类型的数组，对象也可以将其定义为数组，这样的操作形式称为对象数组。对象数组往往是一引用数据类型为主的定义，例如：类、接口，对象数组也有两种定义格式：

- 对象数组动态初始化：类名称 对象数组名称 [] = new 类名称[长度]

- 对象数组的静态初始化：类名称 对象数组名称 [] = new 类名称[]{实例化对象，...}；

**范例** 对象数组的动态初始化：

	class Person {
		private String name;
		private int age;
		public Person(String n, int a) {
			name = n;
			age = a;
		}
		public void setName(String n) {
			 name = n;
		}
		public void setAge(int a) {
			 if(a>0 && a<250) {
				 age = a;
			 }
			 age = 0;
		}
		public String getName() {
			return name;
		}
		public int getAge() {
			return age;
		}
		public String getInfo() {
			return "姓名： " + name + "， 年龄：" + age;
		}
	}
	public class ArrayDemo {
	
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			//动态初始化之后对象数组中的每一个元素都是其对应数据类型的默认值
			Person per [] = new Person [3];//动态初始化
			per[0] = new Person("张三", 1);
			per[1] = new Person("李四", 2);
			per[2] = new Person("王五", 3);
			for(int x=0; x< per.length; x++) {
				System.out.println(per[x].getInfo());
			}
		}
	}

**console：**

	姓名： 张三， 年龄：1
	姓名： 李四， 年龄：2
	姓名： 王五， 年龄：3

**范例** 对象数组静态初始化：

	class Person {
		private String name;
		private int age;
		public Person(String n, int a) {
			name = n;
			age = a;
		}
		public void setName(String n) {
			 name = n;
		}
		public void setAge(int a) {
			 if(a>0 && a<250) {
				 age = a;
			 }
			 age = 0;
		}
		public String getName() {
			return name;
		}
		public int getAge() {
			return age;
		}
		public String getInfo() {
			return "姓名： " + name + "， 年龄：" + age;
		}
	}
	public class ArrayDemo {
	
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			Person per [] = new Person [] {  
				new	Person("张三", 1),
				new Person("李四", 2),
				new Person("王五", 3) 
					};//静态初始化
			for(int x=0; x< per.length; x++) {
				System.out.println(per[x].getInfo());
			}
		}
	}

**console：**

	姓名： 张三， 年龄：1
	姓名： 李四， 年龄：2
	姓名： 王五， 年龄：3

每一个对象可以保存更多的内容，对象数组可以保存的内容比基本数据类型更多，那么应用的也就更多，所有的开发必定都存在有对象数组的概念。

![](https://i.imgur.com/XKUxHXB.png)


## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course20)
