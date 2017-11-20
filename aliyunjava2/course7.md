### 4构造方法与匿名对象###

实例化对象产生格式：

- 1类名称 2对象名称 = 3new 4类名称（）；

对于以上的格式观察组成部分：

- 1类名称：任何的对象都应有对应的类
- 2对象名称:是一个唯一的标记，是操作属性的标记
- 3new: 表示开辟新的堆内存空间
- 4类名称（）: 构造方法

通过以上分析可知，构造方法在使用new实例化对象时就调用了，但是对于构造方法定义需要遵守以下原则：

> 类中一定会至少存在有一个构造方法，如果类中没有明确的定义任何一个构造方法，那么将生成一个无参的，什么都不做的构造方法。

**范例** 定义一个构造方法：

	class Person{
		private String name;
		private int age;
		//构造方法名称与类名称相同，且没有返回值声明
		public Person() {//如果不写此定义也会在编译时生成
			System.out.println("***********");
		}
		public void setName(String n) {
			name = n;
		}
		public void setAge(int a) {
			if(a >= 0 && a<= 250) {
				age = a;
			}else {
				age = 0;
			}
		}
		public String getName() {
			return name;
		}
		public int getAge() {
			return age;
		}
		public void info() {
			System.out.println("name = "+ name + "、age = "+  age);
		}
	}

	public class TestDemo {
		
		public static void main(String[] args) {
			Person per = new Person();
			per.setName("张三");
			per.setAge(-200);
			per.info();
		}
	}

**console**： 

    *********** 
    name = 张三、age = 0

**疑问？** 为什么构造函数中没有返回数据，为什么没有使用void定义呢？	

- 现在的类的组成：属性，普通方法，构造方法
			
		|-属性是在对象开辟堆内存的时候就开辟的空间
		
		|-构造方法是在使用关键字new同时调用的
			|-public Person（）从定义结构上就出现了差异

		|-普通方法是在对象已经实例化完成后（空间开辟了，构造方法执行了）执行的，可以执行多次
			|-public void Person(),命名不标准

- 程序通过定义结构上的差异进行归类的

对于类中可以自动生成的无参构造方法实际上是有一个前提：

> 类中没有定义任何构造方法，相反，如果现在类中已经定义了构造方法，那么此类默认构造方法将不会自动生成。

**范例** 类中定义一个有参构造方法1：
		
	class Person{
		private String name;
		private int age;
		//定义一个有参构造方法，则默认的无参构造方法将不会在编译时生成
		public Person(String n, int a) {
			System.out.println("***********");
		}
		public void setName(String n) {
			name = n;
		}
		public void setAge(int a) {
			if(a >= 0 && a<= 250) {
				age = a;
			}else {
				age = 0;
			}
		}
		public String getName() {
			return name;
		}
		public int getAge() {
			return age;
		}
		public void info() {
			System.out.println("name = "+ name + "、age = "+  age);
		}
	}
	
	public class TestDemo {
		
		public static void main(String[] args) {
			Person per = new Person();
			per.setName("张三");
			per.setAge(-200);
			per.info();
		}
	}


**console**： 

    error：The constructor Person() is undefined

**范例** 类中定义一个有参构造方法2：

	class Person{
		private String name;
		private int age;
		//定义一个有参构造方法，则默认的无参构造方法将不会在编译时生成
		public Person(String n, int a) {
			name = n;//setName(n)
			setAge(a);
		}
		public void setName(String n) {
			name = n;
		}
		public void setAge(int a) {
			if(a >= 0 && a<= 250) {
				age = a;
			}else {
				age = 0;
			}
		}
		public String getName() {
			return name;
		}
		public int getAge() {
			return age;
		}
		public void info() {
			System.out.println("name = "+ name + "、age = "+  age);
		}
	}

	public class TestDemo {
	
		public static void main(String[] args) {
			Person per = new Person("张三",-200);
			per.setName("张三");
			per.setAge(-200);
			per.info();
		}
	}
**console**： 

    name = 张三、age = 0

**构造方法作用：**

- 构造方法的调用和对象内存分配几乎是同步完成的，所以可以利用构造方法设置类中的属性内容
 
- > **构造方法可以为类中的属性进行初始化处理**；

- 通过构造方法设置内容实际上可以避免重复的setter调用
	
	> 在实际开发之中setter方法除了具备有设置内容之外，还可以承担修改数据的操作；

**范例** 通过*setter（）* 修改数据：

	class Person{
		private String name;
		private int age;
		//定义一个有参构造方法，则默认的无参构造方法将不会在编译时生成
		public Person(String n, int a) {
			name = n;//setName(n)
			setAge(a);
		}
		public void setName(String n) {
			name = n;
		}
		public void setAge(int a) {
			if(a >= 0 && a<= 250) {
				age = a;
			}else {
				age = 0;
			}
		}
		public String getName() {
			return name;
		}
		public int getAge() {
			return age;
		}
		public void info() {
			System.out.println("name = "+ name + "、age = "+  age);
		}
	}

	public class TestDemo {
	
		public static void main(String[] args) {
			Person per = new Person("张三",-200);
			per.setName("张三");
			per.setAge(18);
			per.info();
		}
	}

**console**： 

    name = 张三、age = 18

既然构造方法属于方法，那么方法就一定可以进行重载，而构造方法的重载更加简单，因为方法名称不能修改，因此只能够实现参数个数和类型不同这一概念。

**范例** 构造方法重载：
