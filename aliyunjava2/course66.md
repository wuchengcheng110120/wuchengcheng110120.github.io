## [上一页](course65)

## 抽象类的定义与使用（模板设计模式）


抽象类的最大特点在于强制规定了子类的实现结构，那么除了这一特点之外，抽象类更多的情况下还可以起到一个模板的作用。

下面做一个简单的分析。

- 人 = 吃饭 + 睡觉 + 工作 + 学习；

- 猪 = 吃饭 + 睡觉；

- 机器人 = 吃饭 + 工作；

那么现在假设有一个按钮控制（方法），一旦传入了某些指令之后就可以进行相应的处理。

**范例** 定义抽象的行为：

	abstract class Action{//描述的是一个抽象的行为
		public static final int EAT = 1;
		public static final int SLEEP = 5;
		public static final int WORK = 10;
		public void command(int cmd) {
			switch (cmd) {
			case EAT:
				this.eat();
				break;
			case SLEEP:
				this.sleep();
				break;
			case WORK:
				this.work();
				break;
			case WORK + EAT + SLEEP:
				this.work();
				this.sleep();
				this.eat();
				break;
			}
		}
		public abstract void eat();
		public abstract void sleep();
		public abstract void work();
	}

**范例** 定义各个行为的子类

	class Human extends Action{
		public  void eat() {
			System.out.println("人吃饭需要吃熟食，干净的食物！ ");
		};
		public void sleep() {
			System.out.println("人困了就要睡觉。");
		};
		public  void work() {
			System.out.println("人要努力拼搏。");
		};
	}
	class Pig extends Action{
		public  void eat() {
			System.out.println("猪用槽子吃，吃糠...");
		};
		public void sleep() {
			System.out.println("猪在圈里睡.");
		};
		public  void work() {};
	}
	class Robot extends Action{
		public  void eat() {
			System.out.println("机器人补充能量.");
		};
		public void sleep() {};
		public  void work() {
			System.out.println("机器人不停工作.");
		};
	}

**范例** 调用各自的行为操作

	public class TestDemo {
		public static void main(String[] args) {
			fun(new Human());
			fun(new Pig());
			fun(new Robot());
		}
		public static void fun(Action action) {
			action.command(Action.EAT + Action.SLEEP + Action.WORK);
		}
	}

**console：**

	人要努力拼搏。
	人困了就要睡觉。
	人吃饭需要吃熟食，干净的食物！ 
	猪在圈里睡.
	猪用槽子吃，吃糠...
	机器人不停工作.
	机器人补充能量.

实际上通过此程序的定义结构你可以清楚的发现一个问题：

- 抽象类在使用过程中会定义一些固化的模式，它只能接受特定的几种指令；

- 但是每种指令的具体实现由子类负责完成，父类只做了一个方法的约定。

最具有代表性的就是后面要学习的Servlet程序。

1、 抽象类虽然定义了子类必须要做的事情，但是抽象类依然会存在有单继承局限

2、 抽象类的使用必须要通过对象实例化处理

## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course67)
