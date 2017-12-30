## [上一页](course07)
## 泛型（泛型问题引出）

假设需要你定义一个描述坐标的程序类Point类，而这个坐标类中需要提供由两个坐标属性：x，y，对于这两个属性的内容可能有如下的几种选择：

- x = 10，y = 10;

- x = 10.1， y = 20.2;

- x = 东经70度， y = 北纬20度

那么现在首先要解决的问题就是Point类中的x或y的属性类型问题，那么此时需要保存的有int，double，String，所以在java里面只有一种类型可以保存所有的类型：Object

- int自动装箱为Integer，Integer自动向上转型为Object；

- double自动装箱为Double，Double自动向上转型为Object；

- String向上转型为Object；

**范例** 定义Point类：

	class Point{
		private Object x;
		private Object y;
		public Object getX() {
			return x;
		}
		public void setX(Object x) {
			this.x = x;
		}
		public Object getY() {
			return y;
		}
		public void setY(Object y) {
			this.y = y;
		}
	}

**范例** 设置整型坐标：
	
	public class TestDemo {
		public static void main(String[] args) {
			//第一步：设置数据
			Point p = new Point();
			p.setX(10);
			p.setY(20);
			//第二步：取出数据
			int x =(Integer) p.getX();
			int y =(Integer) p.getY();
			System.out.println("x = " + x + "、y = " + y);
		}
	}
**console：**

	x = 10、y = 20


**范例** 设置字符串：

	public class TestDemo {
		public static void main(String[] args) {
			//第一步：设置数据
			Point p = new Point();
			p.setX("东经20度");
			p.setY("北纬10度");
			//第二步：取出数据
			String x =(String) p.getX();
			String y =(String) p.getY();
			System.out.println("x = " + x + "、y = " + y);
		}
	}

**console：**

	x = 东经20度、y = 北纬10度

这一切看起来已经彻底解决了问题，但是现在解决问题的关键是Object，但是问题也即将出现在Object上。

**范例** 观察程序的问题：

	public class TestDemo {
		public static void main(String[] args) {
			//第一步：设置数据
			Point p = new Point();
			p.setX(10.2);//设置坐标
			p.setY("北纬10度");
			//第二步：取出数据
			String x =(String) p.getX();
			String y =(String) p.getY();
			System.out.println("x = " + x + "、y = " + y);
		}
	}
这个时候由于设置方的错误，将坐标内容设置为了double和String，但是接收方不知道，认为还是String接收，所以程序执行后出现如下错误：
	java.lang.ClassCastException

ClassCastException 指的是两个没有关系的对象进行强制转换所带来的异常，这个时候语法并不会对其进行任何的限制，但是执行的时候出现了程序错误，所以得出一个结论：

	向下转型是不安全的操作会带来隐患。





## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course09)
