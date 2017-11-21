## [上一页](course9)


##【第01个代码模型】综合案例：简单Java类 ##

现在假设有这样一个要求，定义一个雇员类，该类中会包含雇员编号、姓名、职位、基本工资、佣金、几个属性信息。

那么这种类成为简单java类，既然是简单java类就有自己明确的开发要求：

> - 类名称应该有意义，可以明确描述出一类事物，例如：Emp、Member、Dept、Dog、Cat；
> 
> - 类中所有属性必须使用private封装，所有的属性必须按要求提供setter、getter方法；
> 
> - 类中可以定义若干个构造方法，但是必须保留有一个无参构造方法；
> 
> - 类中的所有方法都不允许出现任何的System.out语句，所有的输出必须交给调用处完成；
> 
> - 类中应该提供有一个返回类完整信息的方法，这个方法名称暂时为getInfo（）。    

**范例** 编写程序类：
	
	class Emp { //类名称可以明确的描述出某一类事物
		private int empno;
		private String ename;
		private String job;
		private double sal;
		private double comm;
		
		public Emp () {}
		public Emp(int eno, String ena, String j, double s,double c) {
			setEmpno(eno);
			setEname(ena);
			setJob(j);
			setSal(s);
			setComm(c);
		}
		
		public void setEmpno(int eno) {
			empno = eno ;
		}
		public void setEname(String ena) {
			ename = ena;
		}
		public void setJob(String j) {
			job = j;
		}
		public void setSal(double s) {
			sal = s;
		}
		public void setComm(double c) {
			comm  = c;
		}
		public int getEmpno() {
			return empno;
		}
		public String getEname() {
			return  ename;
		}
		public String getJob() {
			return job;
		}
		public double getSal() {
			return sal;
		}
		public double getComm() {
			return comm ;
		}
		public String getInfo() {
			return "empno = " + empno + "\n" +
				   "ename = " + ename + "\n" +
				   "job = " + job + "\n" +
				   "sal = " + sal + "\n" +
				   "comm = " + comm ;  
		}
	}

**范例** 编写测试程序：

	public class TestDemo {
	
		public static void main(String[] args) {
			System.out.println(new Emp(7369,"SMITH","CLERK",800,0.0).getInfo());
		}
	}

**CONSOLE:**

	empno = 7369
	ename = SMITH
	job = CLERK
	sal = 800.0
	comm = 0.0



涵盖了之前所讲解的面向对象概念。

> 以后的开发之中搞的最多的就是简单java类，从基础的web开发，到分布式开发，到处都是简单java类；

> 开发原则一定要记牢




## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course9)

