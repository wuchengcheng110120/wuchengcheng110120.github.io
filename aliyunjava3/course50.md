## [上一页](course49)
## 数字操作类（大数字操作）

数据过大超过了预期的范围。

使用字符串来解决这类问题；

java.math包中提供有两个类：BigInteger、BigDecimal。

java.lang.Object

	java.lang.Number

		java.math.BigInteger

java.lang.Object

	java.lang.Number

		java.math.BigDecimal

**范例** 观察BigInteger：

public BigInteger[] divideAndRemainder(BigInteger val)

	package cn.mldn.demo;
	import java.math.BigInteger;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			BigInteger bigA = new BigInteger("2646131234654613186463131654");
			BigInteger bigB = new BigInteger("56161651646543216849");
			System.out.println("加法计算：" + bigA.add(bigB));
			System.out.println("减法计算：" + bigA.subtract(bigB));
			System.out.println("乘法计算：" + bigA.multiply(bigB));
			System.out.println("除法计算：" + bigA.divide(bigB));
			BigInteger result[] = bigA.divideAndRemainder(bigB);
			System.out.println("商 = " + result[0] + "余数 = " + result[1]);
		}
	}
**console：**

	加法计算：2646131290816264833006348503
	减法计算：2646131178492961539919914805
	乘法计算：148611100611709691976350001352648154315758038246
	除法计算：47116335
	商 = 47116335余数 = 41522781389428003239

**范例** 观察BigDecimal：

	package cn.mldn.demo;
	
	import java.math.BigDecimal;
	import java.math.BigInteger;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			double num = 49466262562.0;
			System.out.println("乘法计算：" + new BigDecimal(num).pow(4546));
		}
	}

这种计算消耗大量CPU资源

在BigDecimal中有一个四舍五入的实现

public BigDecimal divide(BigDecimal divisor,
                         int scale,
                         RoundingMode roundingMode)

进位模式： public static final int ROUND_HALF_UP

	class MyMath{
		public static double round(double num,int scale) {
			return new BigDecimal(num).divide(new BigDecimal(1), scale, BigDecimal.ROUND_HALF_UP).doubleValue();
		}
	}

	public class TestDemo {
		public static void main(String[] args) throws Exception {
			System.out.println(MyMath.round(23234.2363, 2));
		}
	}

**console：**

	23234.24

关于四舍五入的处理实际上有以上两类做法。

在实际开发过程中，在做复杂逻辑计算式需要寻找更高效的开发包；






## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course51)
