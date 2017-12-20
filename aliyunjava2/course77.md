## [上一页](course76)

## Object类（接收引用数据类型）

在之前已经分析了Object可以接收任意的对象，因为从定义的结构上来讲，Object是所有类的父类，但Object的概念并不仅仅局限于此，它可以接收所有的引用数据类型，包括：数组、接口。

**范例** 使用Object来接收数组对象：

	public class TestDemo {
		public static void main(String[] args) {
			//利用Object接收数组对象， 向上转型
			Object obj = new int[] {1,2,3};
			// 向下转型，需要强制类型转换
			int data[] = (int[]) obj;
			for (int i = 0; i < data.length; i++) {
				System.out.print(data[i] + "、");
			}
		}
	}
**console：**

	1、2、3、

而Object可以接收接口更是Java中的强制要求，因为接口本身是不可能继承任何类的，所以这种类型的接收就是自己的规定。

**范例** 使用Object接收接口对象：

	interface IMessage{
	}
	class MessageImpl implements IMessage{
		public  String toString() {//Object 类的方法
			return "www.mldn.cn";
		}
	}
	public class TestDemo {
		public static void main(String[] args) {
			IMessage msg = new MessageImpl();//子类向父接口转型
			Object obj = msg;//接口向Object转型
			System.out.println(obj);
			IMessage temp = (IMessage)obj;//强制转换
		}
	}

**console：**

	www.mldn.cn

Object真正达到了参数的统一，如果一个类希望可以接收所有的数据类型，就使用Object完成


## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course78)
