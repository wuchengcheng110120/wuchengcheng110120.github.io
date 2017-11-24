## [上一页](course14)
## 6.7 数组案例：数组数据统计

假设给出一个数组，求出该数组的最大值、最小值、平均值、总和，通过循环来完成。

**范例** 求一个数组统计数据基本实现：

	public class ArrayDemo {
	
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			int data [] = new int [] {1,2,3,4,66,5,6,7,8,9};
			
			int max = data[0];
			int min = data[0];
			int sum = 0;
			
			
			for (int x = 0; x< data.length; x++) {
				
				sum += data[x];
				
				if(data[x] > max)
					max = data[x];
				if(data[x] < min)
					min = data[x];		
			}
			System.out.println("最大值： " + max);
			System.out.println("最小值： " + min);
			System.out.println("数据总和： " + sum);
			System.out.println("平均值： " + sum/(double)data.length);	
		}
	}

**console：**

	最大值： 66
	最小值： 1
	数据总和： 111
	平均值： 11.1

此时实现了需要的功能，但是随之主方法中的代码过多，主方法实际上相当于客户端调用，里面的代码越简单越好。

**范例** 改进代码：

	public class ArrayDemo {
	
		public static void main(String[] args) {
			// TODO Auto-generated method stub
			int data [] = new int [] {1,2,3,4,66,5,6,7,8,9};
			double result[] = stat(data);
		
			System.out.println("最大值： " + (int)result[0]);
			System.out.println("最小值： " + result[1]);
			System.out.println("数据总和： " + result[2]);
			System.out.println("平均值： " + result[3]);	
		}
		//此时需要返回四个数据，一个方法只能返回一个数据类型，只能用数组返回
		//数组[0]为最大值，数组[1]为最小值，数组[2]为数据总和，数组[3]为平均值
		public static double[] stat(int data[]) {
			double retData[] = new double [4];
			
			retData[0] = data[0];
			retData[1] = data[0];
			retData[2] = 0;		
			for (int x = 0; x< data.length; x++) {
				
				retData[2] += data[x];
				
				if(data[x] > retData[0]) {
					retData[0] = data[x];
				}
				if(data[x] < retData[1]) {
					retData[1] = data[x];		
				}
			}
			
			retData[3] = retData[2]/(double)data.length;
			return retData;
		}
	}

**console：**

	最大值： 66
	最小值： 1.0
	数据总和： 111.0
	平均值： 11.1

在进行整个程序开发的时候，主方法不要涉及到过于复杂的程序逻辑，只需要关注结果。

## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course16)
