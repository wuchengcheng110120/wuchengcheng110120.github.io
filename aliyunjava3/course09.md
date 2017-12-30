## [上一页](course08)
## 泛型（泛型实现）

所谓的泛型指的就是在类定义的时候并不会设置类中的属性或方法中的参数的具体类型，而是在类使用的时候进行定义。所以想要进行这种泛型的操作，就必须做一个类型标记的声明。

**范例** 定义Point类：

	class Point<T>{		//T表示参数，是一个占位的标记
		//在Point类定义的时候完全不知道x和y的实行是什么，而由使用者来决定
		private T x;
		private T y;
		public T getX() {
			return x;
		}
		public void setX(T x) {
			this.x = x;
		}
		public T getY() {
			return y;
		}
		public void setY(T y) {
			this.y = y;
		}
	}
	
	public class TestDemo {
		public static void main(String[] args) {
			//第一步：设置数据
			Point<String> p = new Point<>();
			p.setX("东经20度");//设置坐标
			p.setY("北纬10度");
			//第二步：取出数据
			String x = p.getX(); 	//避免了向下转型
			String y = p.getY();	//避免了向下转型
			System.out.println("x = " + x + "、y = " + y);
		}
	}

当开发的程序可以避免向下转型，也就意味着这种安全隐患被消除了。

泛型不设置默认按Object处理，尽量不要去使用向下转型。


## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course10)
