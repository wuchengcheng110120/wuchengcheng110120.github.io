## [last page](course2)


### 2.2 类与对象（类与对象定义） ###

所有的对象只有实例化之后才可以真正使用，而对象的使用都是围绕着类来进行的那么此时使用就有两种形式：
	
- 调用类中的属性： 对象.属性 = 内容；
- 调用类中的方法： 对象.方法（）；

		class Person{
		
			String name;
			int age;
			public void info() {
				System.out.println("name = "+ name + "、age = "+  age);
			}
		}

		public class TestDemo {
	
			public static void main(String[] args) {
				// TODO Auto-generated method stub
				//类名称 对象名称 = new 类名称（）；
				Person person = new Person();
				person.name = "张三";//设置对象中的属性
				person.age = 25;//设置对象中的属性
				person.info();//调用类中的方法
						
			}
		}



## [back to the list](https://wuchengcheng110120.github.io/learnJava)
## [next page](course4)
