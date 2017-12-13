## [上一页](course58)

## 综合案例：数组操作（定义Array父类）


现在要求定义一个数组（整型数据）的操作类，在这个类中有如下几个要求：

- 该数组的大小由类创建对象的时候动态决定；

- 可以通过类向数组中进行数据保存，保存的时候需要考虑数组的大小问题

- 如果发现数组长度不足，则可以进行数组长度的动态扩充；

- 可以取得数组的全部数据（增加顺序）；

而后再这基础之上要求继续扩展两个派生类：

- 可以进行数组的排序处理；

- 可以进行数组的反转处理；


		class Array {//定义一个专门进行数组操作的类
			private int data [];//定义一个整型数组，大小由外部决定
			private int foot = 0;//进行数组的角标操作
			public Array(int len){//如果想要使用Array类必须设置数组大小
				if (len > 0) {//一个正常的数组大小
					this.data = new int [len];//开辟新数组
				}else {
					this.data = new  int [0];
				}
			}
			//该方法主要功能是向数组里面进行数据的保存
			public boolean add(int num){
				if (this.foot >= this.data.length) {//没空间了
					return false;
				}
				//先进性数组的数据保存，而后foot的值+1
				this.data[this.foot ++] = num;
				return true;
			}
			public int[] getData(){
				return this.data;
			}
			//动态扩展，如果此时传入一个3，则表示在原有的基础上数组长度追加3（5+3=8）
			public void inc(int num){
				int newData [] = new int [this.data.length + num];
				System.arraycopy(data, 0, newData,0 , data.length);
				this.data = newData;//改变数组指向
			}
		}
		public class TestDemo {
			public static void main(String[] args) {
				// TODO Auto-generated method stub
				Array arr = new Array(5);
				System.out.println(arr.add(3));
				System.out.println(arr.add(1));
				System.out.println(arr.add(2));
				System.out.println(arr.add(8));
				System.out.println(arr.add(6));
				arr.inc(3);
				System.out.println(arr.add(10));
				System.out.println(arr.add(20));
				System.out.println(arr.add(30));
				int[] result = arr.getData();
				for (int i = 0; i < result.length; i++) {
					System.out.print(result[i] + "、" );
				}
			}
		}

**console：**

	true
	true
	true
	true
	true
	true
	true
	true
	3、1、2、8、6、10、20、30、


Array类的定义只需要根据自己的需求完成所需要的功能即可，按照标准做即可。

![](https://i.imgur.com/nMqOYJZ.png)

## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course60)
