## [上一页](course56)

## 覆写（属性覆盖）

当子类定义了和父类属性名称完全相同的属性的时候就称为属性覆盖。

	class Person{
		public String info = "www.mldn.cn";
	}
	class Student extends Person{
		//因为此时按照就近取用的原则，肯定找被覆盖的属性
		public int info = 100;//属性名称相同
		public void printInfo() {
			System.out.println(info);
		}
	}
	public class TestDemo {
		public static void main(String args[]) {
			Student stu = new Student(); //实例化子类
			stu.printInfo();
		}
	}

**console：**

	100

这种操作本身是没有任何意义的，其核心原因在于：所有类中的属性都要求使用private封装，所有子类并不知道父类的属性，所以属性覆盖并没有意义。

结论：在定义属性时，属性重名是危险操作。

## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course58)
