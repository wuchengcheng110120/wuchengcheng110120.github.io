## [上一页](course59)

## 综合案例：数组操作（SortArray排序子类）

如果要进行排序的处理操作，那么肯定在取得了全部数据的时候里面的内容因该是排序好的，同时在该类操作的过程之中应该继续具备有：数据追加、数组扩充、取得全部数据（父类中的getData（）方法作为一个获取数据的标准。）。

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
	//这样可以继承所有已经存在的操作方法
	class SortArray extends Array{
		//父类中现在并没有无参构造方法，所以此时的子类必须明确的调用父类中的构造方法
		public SortArray(int num){
			super(num);//父类中支持数组创建了
		}
		//父类中的取得数据的方法名称很标准，但是功能不足，又希望继续使用这个方法名称，
		//那么就需要对方法进行扩充，扩充就是方法覆写的核心作用
		public int[] getData(){
			java.util.Arrays.sort(super.getData());
			return super.getData();//引用传递
		}
	}
	
	public class TestDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			SortArray arr = new SortArray(5);
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
	1、2、3、6、8、10、20、30、

也就是说不同的子类一定要针对于方法进行部分的扩展。

## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course61)

