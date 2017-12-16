## [上一页](course60)

## 综合案例：数组操作（ReverseArray反转子类）

反转子类的最大特点在于，取得的数据使其保存顺序的相反内容。整体的实现风格实际上和排序数组子类是一样的。

**范例** 反转子类：

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
	
	class ReverseArray extends Array{
		//必须知道数组大小
		public ReverseArray(int len) {//必须明确父类调用
			super(len);
		}
		public int[] getData(){
			int center = super.getData().length/2;
			int head = 0 ; 
			int tail = super.getData().length-1;
			for (int i = 0; i < center; i++) {
				int temp = super.getData()[head];
				super.getData()[head] = super.getData()[tail];
				super.getData()[tail] = temp;
				head++;
				tail--;
			}
			return super.getData();//引用传递
		}
	}
	
	public class TestDemo {
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			ReverseArray arr = new ReverseArray(5);
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
	30、20、10、6、8、2、1、3、

本程序完美的表现出来了对继承的概念诠释及覆写的核心意义。


## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course62)
