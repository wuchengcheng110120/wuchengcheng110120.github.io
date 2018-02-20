## [上一页](course130)
##  【第18个代码模型】 List集合接口（ArrayList子类）

ArrayList是一个针对List接口进行的数组操作实现，下面首先利用ArrayList做一些List基本操作。

范例： 观察List基本处理：

	package cn.mldn.demo;
	
	import java.util.ArrayList;
	import java.util.List;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			List<String> all = new ArrayList<String>(); // 此时集合里面只允许保存String数据类型
			all.add("Hello") ;
			all.add("Hello") ; //重复数据
			all.add("World") ;
			System.out.println(all);
		} 	
	}

**console：**

	[Hello, Hello, World]

通过此时的观察可以证实：List是允许保存重复数据的。

**范例** 其他操作：

	package cn.mldn.demo;
	
	import java.util.ArrayList;
	import java.util.List;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			List<String> all = new ArrayList<String>(); // 此时集合里面只允许保存String数据类型
			System.out.println(all.size() + "、" + all.isEmpty());
			all.add("Hello") ;
			all.add("Hello") ; //重复数据
			all.add("World") ;
			all.remove("Hello");
			System.out.println(all.size() + "、" + all.isEmpty());
			System.out.println(all.contains("ABC"));
			System.out.println(all.contains("World"));
			System.out.println(all);
		} 	
	}

**console：**

	0、true
	2、false
	false
	true
	[Hello, World]

List本身有一个好的支持：它本身存在有一个get()方法，那么利用这个get()方法可以结合索引取出数据。

**范例** 观察List的get()操作：

	package cn.mldn.demo;
	
	import java.util.ArrayList;
	import java.util.List;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			List<String> all = new ArrayList<String>(); // 此时集合里面只允许保存String数据类型
			all.add("Hello") ;
			all.add("Hello") ; //重复数据
			all.add("World") ;
			for (int x = 0; x < all.size(); x++) {
				System.out.println(all.get(x));
			}
		} 	
	}
**console：**

	Hello
	Hello
	World

但是千万要记住，get()方法是List子接口的，如果你现在使用的不是List而是Connection（虽然这种情况大多数不会发生），那么对于此时的数据取出你只能将集合变为对象数组来操作：

**范例** 通过Connection进行输出处理

	package cn.mldn.demo;
	
	import java.util.ArrayList;
	import java.util.Arrays;
	import java.util.Collection;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			Collection<String> all = new ArrayList<String>(); // 此时集合里面只允许保存String数据类型
			all.add("Hello") ;
			all.add("Hello") ; //重复数据
			all.add("World") ;
			// 操作以Object形式返回，那么就有可能需要进行向下转型，那么就有可能造成ClassCastException的安全隐患
			Object [] result = all.toArray(); //变成Object对象数组
			System.out.println(Arrays.toString(result));
		} 	
	}

这种操作尽量回避，不到万不得已尽量不要使用。




## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course132)
