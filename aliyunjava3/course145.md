## [上一页](course144)
##  【第21个代码模型】 Map集合（ConcurrentHashMap子类）

ConcurrentHashMap的特点 = Hashtable的线程安全型 + HashMap的高性能，在使用ConcurrentHashMap处理的时候既能够保证多个线程更新数据的同步，又可以保证很高效的查询速度。

首先来观察ConcurrentHashMap的子类定义：

	public class ConcurrentHashMap<K,V>
	extends AbstractMap<K,V>
	implements ConcurrentMap<K,V>, Serializable

**范例** 使用ConcurrentHashMap：

	package cn.mldn.demo;
	
	import java.util.Map;
	import java.util.concurrent.ConcurrentHashMap;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			Map<Integer, String> map = new ConcurrentHashMap<Integer,String>();
			map.put(3, "MLDNJava");
			map.put(1, "Hello");
			map.put(1, "World"); //key重复
			map.put(2, "MLDN");
			System.out.println(map);
		} 	
	}
**console：**

	{1=World, 2=MLDN, 3=MLDNJava}

于是现在就需要分析一下ConcurrentHashMap的工作原理。

如果现在采用算法，将大量数据平均分在不同的桶（数据区域），这样在进行数据查找的时候就可以避免掉这种全部的数据扫描。

**范例**  数据分桶：

	public class TestDemo {
		public static void main(String[] args) throws Exception {
			for (int x = 0; x < 10; x++) {
				new Thread(()->{
					Random rand = new Random();
					int temp = rand.nextInt(9999);
					int result = temp % 3;
					switch (result) {
					case 0:
						System.out.println("【第0桶】" + temp);
						break;
					case 1:
						System.out.println("【第1桶】" + temp);
						break;
					case 2:
						System.out.println("【第2桶】" + temp);
						break;
	
					}
				}) .start();
			}
		} 	
	}
**console：**

	【第1桶】3850
	【第1桶】382
	【第2桶】5150
	【第2桶】131
	【第2桶】5099
	【第2桶】5369
	【第0桶】6396
	【第0桶】4029
	【第2桶】4712
	【第0桶】9561

采用了分桶之后每一个数据中必须有一个明确的分桶标记，很明显在这里使用的是hashCode()。

![](http://ww4.sinaimg.cn/large/0060lm7Tly1fowax3ghojj30v90hjn1r.jpg)

![](http://ww2.sinaimg.cn/large/0060lm7Tly1foway4ounmj30v80hc43d.jpg)

![](http://ww2.sinaimg.cn/large/0060lm7Tly1fowb0sj5unj30vb0hg45z.jpg)

![](http://ww3.sinaimg.cn/large/0060lm7Tly1fowb5yfv3ij30v40h9gtp.jpg)


## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course146)
