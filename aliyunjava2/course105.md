## [上一页](course104)

## 【第05个代码模型】综合案例：宠物商店

现在要求建立一个宠物商店，里面可以进行要销售宠物的上架、下架以及关键字查询。要求：描述出程序的关系即可。

宠物信息要求三项：名字、年龄、颜色。

那么此时对应的关系：一个宠物商店会有多种宠物。如果按照表设计来讲应该属于一对多关系映射，但是现在的问题是一方应该是宠物商店，而多方应该是宠物，但是宠物又分为猫、狗、猪、鱼等等。

![](https://s1.ax1x.com/2017/12/28/xvy11.png)

1、 建立宠物标准：

	interface Pet{//定义宠物
		public String getName();
		public String getColor();
		public int getAge();
	}

2、对于宠物商店，只关心宠物的标准而不关心是哪种宠物：

	class PetShop{
		private Link pets = new Link();//开辟一个新的链表，保存多个宠物信息
		public void add(Pet pet) {// 上架的宠物
			this.pets.add(pet); // 向链表中保存数据
		}
		public void delete(Pet pet) {// 下架宠物
			this.pets.remove(pet);
		}
		public Link getPets() {//取得全部的宠物
			return this.pets;
		}
		public Link Search(String keyWord) {
			Link result = new Link(); // 保存查询结果
			Object [] data = this.pets.toArray();
			for (int i = 0; i < data.length; i++) {
				Pet pet = (Pet) data[i];
				if (pet.getName().contains(keyWord) || pet.getColor().contains(keyWord)) {
					result.add(pet); // 满足查询结果
				}else {
					
				}
				return result;
			}
		}
	}
3、定义宠物狗：

	class Dog implements Pet {
		private String name;
		private String color;
		private int age;
		public Dog(String name, String color, int age) {
			this.age =age;
			this.color = color;
			this.name =name;
		}
		public String toString() {
			return "【狗】名字：  " + this.name + ", 颜色 ： " + this.color + 
					", 年龄 ： " + this.age; 
		}
		public String getName() {
			return this.name;
		}
		public String getColor() {
			return this.color;
		}
		public int getAge() {
			return this.age;
		}
		public boolean equals(Object obj) {
			if (obj == null) {
				return false;
			}
			if (this == obj) {
				return true;
			}
			if (!(obj instanceof Dog)) {
				return false;
			}
			Dog pet = (Dog) obj;
			return this.name.equals(pet.name) && this.age == pet.age && this.color.equals(pet.color) ;
		}
	}

4、定义宠物猫：

	class Cat implements Pet {
		private String name;
		private String color;
		private int age;
		public Cat(String name, String color, int age) {
			this.age =age;
			this.color = color;
			this.name =name;
		}
		public String toString() {
			return "【猫】名字：  " + this.name + ", 颜色 ： " + this.color + 
					", 年龄 ： " + this.age; 
		}
		public String getName() {
			return this.name;
		}
		public String getColor() {
			return this.color;
		}
		public int getAge() {
			return this.age;
		}
		public boolean equals(Object obj) {
			if (obj == null) {
				return false;
			}
			if (this == obj) {
				return true;
			}
			if (!(obj instanceof Cat)) {
				return false;
			}
			Cat pet = (Cat) obj;
			return this.name.equals(pet.name) && this.age == pet.age && this.color.equals(pet.color) ;
		}
	}

5、 编写测试程序

	interface Pet{//定义宠物
		public String getName();
		public String getColor();
		public int getAge();
		
	}
	class PetShop{
		private Link pets = new Link();//开辟一个新的链表，保存多个宠物信息
		public void add(Pet pet) {// 上架的宠物
			this.pets.add(pet); // 向链表中保存数据
		}
		public void delete(Pet pet) {// 下架宠物
			this.pets.remove(pet);
		}
		public Link getPets() {//取得全部的宠物
			return this.pets;
		}
		public Link Search(String keyWord) {
			Link result = new Link(); // 保存查询结果
			Object [] data = this.pets.toArray();
			for (int i = 0; i < data.length; i++) {
				Pet pet = (Pet) data[i];
			if (pet.getName().contains(keyWord) || pet.getColor().contains(keyWord)) {
					result.add(pet); // 满足查询结果
				}
			}	
			return result;
		}
	}
	class Dog implements Pet {
		private String name;
		private String color;
		private int age;
		public Dog(String name, String color, int age) {
			this.age =age;
			this.color = color;
			this.name =name;
		}
		public String toString() {
			return "【狗】名字：  " + this.name + ", 颜色 ： " + this.color + 
					", 年龄 ： " + this.age; 
		}
		public String getName() {
			return this.name;
		}
		public String getColor() {
			return this.color;
		}
		public int getAge() {
			return this.age;
		}
		public boolean equals(Object obj) {
			if (obj == null) {
				return false;
			}
			if (this == obj) {
				return true;
			}
			if (!(obj instanceof Dog)) {
				return false;
			}
			Dog pet = (Dog) obj;
			return this.name.equals(pet.name) && this.age == pet.age && this.color.equals(pet.color) ;
		}
	}
	
	class Cat implements Pet {
		private String name;
		private String color;
		private int age;
		public Cat(String name, String color, int age) {
			this.age =age;
			this.color = color;
			this.name =name;
		}
		public String toString() {
			return "【猫】名字：  " + this.name + ", 颜色 ： " + this.color + 
					", 年龄 ： " + this.age; 
		}
		public String getName() {
			return this.name;
		}
		public String getColor() {
			return this.color;
		}
		public int getAge() {
			return this.age;
		}
		public boolean equals(Object obj) {
			if (obj == null) {
				return false;
			}
			if (this == obj) {
				return true;
			}
			if (!(obj instanceof Cat)) {
				return false;
			}
			Cat pet = (Cat) obj;
			return this.name.equals(pet.name) && this.age == pet.age && this.color.equals(pet.color) ;
		}
	}
	
	public  class PetShopDemo {
	
		public static void main(String[] args) {
			PetShop ps = new PetShop();
			ps.add(new Dog("黑狗", "白色", 1));
			ps.add(new Dog("金毛", "黄色", 2));
			ps.add(new Dog("腊肠", "金色", 1));
			ps.add(new Dog("拉布拉多", "金色", 1));
			ps.add(new Cat("加菲猫", "金色", 1));
			ps.add(new Cat("波斯猫", "白色", 1));
			ps.delete(new Dog("腊肠", "金色", 1));
			Link all = ps.Search("金");
			Object [] data =all.toArray();
			for (int i = 0; i < data.length; i++) {
				System.out.println(data[i]);
			}
		}
	}

实际之中这种形式的代码在生活中随处可见：

- 一个公园可以由多种植物；

- 动物园可以有多种动物；

- 一个衣柜可以有多件衣服；

-一个人可以吃多种食物；

进行开发过程中一切以接口设计为主




## [返回目录](https://wuchengcheng110120.github.io/learnJava)

