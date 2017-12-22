## [上一页](course83)

## 访问控制权限

private是一种访问控制权限，只是封装的一部分，在java中提供有四种访问控制权限：private、default、protected、public，而这四种访问控制权限定义如下：

No. | 范围 | private | default | protected | public
 -|-| -|-|-|-|
 1、 | 同一包中的同一类 | √ | √ | √ | √
 2、 | 同一包中的不同类 | × | √ | √ | √ 
 3、 | 不同包中的子类 | × | × | √ | √
 4、 | 不同包中的非子类 | × | × | × | √

实际上public永远都能够访问，但是对于封装而言主要是有三个权限：private、default、protected。

**范例** 观察protected访问权限：

	package cn.mldn.demo.a;
	
	class Info {//此时出现的是protected访问权限
		protected String str = "www.mldn.cn";
	}

**范例** 定义另外一个包进行该类的继承：

	package cn.mldn.demo.b;
	import cn.mldn.demo.a.Info;
	public class SubInfo extends Info {//Info的子类
		public void print() {
			System.out.println(super.str);//在父类中属于protected权限
		}
	}

**范例** 定义测试程序类：

	package cn.mldn.testab;
	import cn.mldn.demo.b.SubInfo;
	public class TestInfo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			new SubInfo().print();
		}
	}

**console：**

	www.mldn.cn	

现在SubInfo虽然与Info属于不同的开发包，但是毕竟是其子类，所以可以访问，但是反过来，如果想要在TestInfo中直接使用Info类（非子类），就会出现错误。

	package cn.mldn.testab;
	import cn.mldn.demo.a.Info;;
	public class TestInfo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			System.out.println(new Info().str);
		}
	}

str是protected权限此处一定无法访问：
		
	Exception in thread "main" java.lang.Error: Unresolved compilation problem: 
		The field Info.str is not visible

结论：关于权限的选择

- 对于封装的描述90%使用的都是private，只有很少情况会使用protected，这两种都叫封装；

-属性都使用private，方法都使用public；

封装性主要就是private、default、protected三个权限的使用。


## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course85)
