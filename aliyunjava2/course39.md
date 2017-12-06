## [上一页](course38)

##  引用传递实际应用

引用传递可以更好的表示现实世界的抽象。

例如，描述这样一种关系：一个人有一辆车或没有汽车。很明显，现在应该有两个实体类：人（Member）、车（Car）。

**范例**  如下设计：

	class Member {
		private String name;
		private int age;
		//if car == null, 表示这个人没有车
		private Car car;//一个人可以有车
		public Member(String name, int age) {
			this.name = name;
			this.age = age;
		}
		
		public void setCar(Car car) {
			this.car = car;
		}
		
		public Car getCar() {
			return this.car;
		}
		public String getMemberInfo() {
			return "【Member】 name = "+ this.name + ", age = " + this.age;
		}
	}
	
	class Car {
		private String name;
		private double price;
		private Member member;
		public Car(String name, double price) {
			this.name = name;
			this.price = price;
		}
		public void setMember(Member member) {
			this.member = member;
		}
		
		public Member getMember() {
			return this.member;
		}
		
		
		public String getCarInfo() {
			return "【Car】 name = " + this.name + ", price " + this.price;
		}
	}
	
	public class TestDemo {
		public static void main(String args[]) {
			//第一步：根据关系设置相应的数据
			//1. 分别创建各自对象的实例
			Member mem = new Member("于博", 30);
			Car car = new Car("法拉利", 5000000.0);
			//2.设置对象间的引用关系
			mem.setCar(car);
			car.setMember(mem);
			//第二步：根据关系取出数据
			//3.通过人可以找到车
			System.out.println(mem.getMemberInfo());
			System.out.println(mem.getCar().getCarInfo());
			//4.通过车找到人
			System.out.println(car.getMember().getMemberInfo());
		}
	}

**console：**

	【Member】 name = 于博, age = 30
	【Car】 name = 法拉利, price 5000000.0
	【Member】 name = 于博, age = 30

进一步设计，member会有后代，后代也会有车。

- 建立孩子类，建立孙子类；

- 直接在Member类里面建立一个新的后代属性，孩子的类型就是Member；


**范例**  进一步设计：

	class Member {
		private String name;
		private int age;
		private Member child;
		//if car == null, 表示这个人没有车
		private Car car;//一个人可以有车
		public Member(String name, int age) {
			this.name = name;
			this.age = age;
		}
		
		public void setChild(Member child) {
			this.child =child;
		}
		public Member getChild() {
			return this.child;
		}
		
		public void setCar(Car car) {
			this.car = car;
		}
		
		public Car getCar() {
			return this.car;
		}
		public String getMemberInfo() {
			return "【Member】 name = "+ this.name + ", age = " + this.age;
		}
	}
	
	class Car {
		private String name;
		private double price;
		private Member member;
		public Car(String name, double price) {
			this.name = name;
			this.price = price;
		}
		public void setMember(Member member) {
			this.member = member;
		}
		
		public Member getMember() {
			return this.member;
		}
		
		
		public String getCarInfo() {
			return "【Car】 name = " + this.name + ", price " + this.price;
		}
	}
	
	public class TestDemo {
		public static void main(String args[]) {
			//第一步：根据关系设置相应的数据
			//1. 分别创建各自对象的实例
			Member mem = new Member("于博", 30);
			Car car = new Car("法拉利", 5000000.0);
			Member chd = new  Member("于三", 8);
			Car cc = new Car("玛莎拉蒂", 3.0);
			
			//2.设置对象间的引用关系
			mem.setCar(car);
			mem.setChild(chd);
			chd.setCar(cc);
			car.setMember(mem);
			
			//第二步：根据关系取出数据
			//3.通过人可以找到车
			System.out.println(mem.getMemberInfo());
			System.out.println(mem.getCar().getCarInfo());
			//4.通过车找到人
			System.out.println(car.getMember().getMemberInfo());
			//5.通过人找到孩子
			System.out.println(mem.getChild().getMemberInfo());
			//6.通过人找到孩子的车
			System.out.println(mem.getChild().getCar().getCarInfo());
		}
	}

**console：**

	【Member】 name = 于博, age = 30
	【Car】 name = 法拉利, price 5000000.0
	【Member】 name = 于博, age = 30
	【Member】 name = 于三, age = 8
	【Car】 name = 玛莎拉蒂, price 3.0

这些关系的配置可以很好的反映现实生活。

如果现在还想再进行扩展，实际上也可以更好的描述出实际的组成关系，例如：一台电脑由显示器、主机、硬盘、键盘、鼠标、CPU、主板、内存所组成，那么这样的关系如何表示？

	class Computer{
		private Display[] displays;
		private MainFrame mainFrame;
		private Keyboard[] keyboards;
		private Mouse[] mouses;
	}
	class Display{}
	class MainFrame{
		private Motherboard motherboard;
	}
	class Disk{}
	class Keyboard{}
	class Mouse{}
	class Motherboard{
		private Cpu[] cpus;
		private Memory[] memories;
		private Disk[] disks;
		private Graphicscard[] graphicscards;
	}
	class Cpu{}
	class Memory{}
	class Graphicscard{}
	
	public class TestDemo {
		public static void main(String args[]) {
			Computer computer = new Computer();
		}
	}

只有将这些细小的类合并到一起才能够描述出一个完整的概念，而且在实际生活之中，这些细小的组成部分都可以进行替代替换。所以这样的设计就属于合成设计模式。


以后的项目开发过程之中，所使用到的类基本上都是要求由开发者自己来进行定义。这里面使用的都是引用传递的概念。

## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course40)
