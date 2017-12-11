## [上一页](course52)

## 继承的定义与使用（继承问题的引出）

Java的第二大特点就是继承，继承的主要作用在已有的基础上进行功能的扩充，

如果想要更好的理解继承的概念，按照已有的概念来定义两个类：表示人的类和人的学生类。


**范例**  继承问题的引出：
			
	class Person{
		private String name;
		private int age;
		public void setName(String name){
			this.name = name;
		}
		public void setAge(int age){
			this.age = age;
		}
		public String getName(){
			return this.name;
		}
		public int getAge(){
			return this.age;
		}
	}
	
	class Student{
		private String name;
		private int age;
		private String school;
		public void setName(String name){
			this.name = name;
		}
		public void setAge(int age){
			this.age = age;
		}
		public void setSchool(String school){
			this.school = school;
		}
		public String getName(){
			return this.name;
		}
		public int getAge(){
			return this.age;
		}
		public String getSchool(){
			return this.school;
		}
	}

以上的代码模式就是之前所学习的单独的简单java类模式，通过不断地编写，就可以发现，程序中有许多重复的代码，而且从概念上讲一个学生一定是一个人，而学生和人相比是更加具体的描述，描述的范围更小，具备的属性更多，方法也会更多，所以Student类是Person类的扩充。

这个时候想要消除结构定义上的重复，就必须用继承来完成。

## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course54)

