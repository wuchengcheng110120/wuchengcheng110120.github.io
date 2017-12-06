## [上一页](course39)

##  【第03个代码模型】综合案例：数据表与简单JAVA类（一对多）

Oracle学习中中涉及两张数据表：emp、dept；
- emo表：empno、ename、job、sal、comm、mgr、deptno

- dept表：deptno、dname、loc

要求可以通过程序描述出如下的对应关系：

- 一个部门有多个雇员，并且可以输出一个部门的完整信息（包括雇员信息）；

- 可以根据一个雇员找到雇员对应的领导信息和雇员所在部门的信息；


【实际开发中简单java类设计原则】

通过简单java类的开发和数据表的使用，应该能发现两者之间存在的对应关系：

- 简单java类的名称 = 实体表名称 ；

- 简单java类的属性 = 实体表的字段；

- 简单java类的一个对象 = 表的一行记录；

- 对象数组 = 表的多行记录；

- 外键关系 = 引用配置；

1 、 先按照给定的关系将所有的基础字段转化为类

	class Emp {
		private int empno;
		private String ename;
		private String job;
		private double sal;
		private double comm;
		public Emp() {}
		public Emp(int empno, String ename, String  job, double sal, double comm) {
			this.empno = empno;
			this.ename = ename;
			this.job = job;
			this.sal = sal;
			this.comm =comm;
		}
		public String getInfo() {
			return "【EMP】 empno = " + this.empno + ", ename = " + this.ename +
					", job = " + this.job + ", sal = " + this.sal + ", comm  = "+ this.comm ;
		}		
	}
	
	class Dept {
		private int deptno;
		private String dname;
		private String loc;
		public Dept() {}
		public Dept(int deptno, String dname, String loc) {
			this.deptno = deptno;
			this.dname = dname;
			this.loc = loc;
		}
		public String getInfo() {
			return "【DEPT】  deptno = " + this.deptno + ", dname = " + this.dname + 
					", loc = " + this.loc ;
		}
	}

2 、随后要进行关系设计

- 一个雇员属于一个部门，需要追加部门引用；

- 一个雇员属于一个领导，领导一定是自身关联，自身引用；

- 一个部门有多个雇员，需要一个对象数组来描述雇员信息；


		class Emp {
			private int empno;
			private String ename;
			private String job;
			private double sal;
			private double comm;
			private Emp mgr ; //描述雇员领导
			private Dept dept;//描述雇员所在部门
			
			public Emp() {}
			public Emp(int empno, String ename, String  job, double sal, double comm) {
				this.empno = empno;
				this.ename = ename;
				this.job = job;
				this.sal = sal;
				this.comm =comm;
			}
			
			public void setMgr(Emp mgr) {
				this.mgr = mgr ;
			}
			
			public Emp getMgr() {
				return this.mgr;
			}
			public void setDept(Dept dept) {
				this.dept = dept ;
			}
			public Dept getDept() {
				return this.dept;
			}
			public String getInfo() {
				return "【EMP】 empno = " + this.empno + ", ename = " + this.ename +
						", job = " + this.job + ", sal = " + this.sal + ", comm  = "+ this.comm ;
			}		
		}

		class Dept {
			private int deptno;
			private String dname;
			private String loc;
			private Emp [] emps;
			
			public Dept() {}
			public Dept(int deptno, String dname, String loc) {
				this.deptno = deptno;
				this.dname = dname;
				this.loc = loc;
			}
			public void setEmps(Emp [] emps) {
				this.emps = emps;
			}
			public Emp[] getEmps() {
				return this.emps;
			}
			
			public String getInfo() {
				return "【DEPT】  deptno = " + this.deptno + ", dname = " + this.dname + 
						", loc = " + this.loc ;
			}
		}
3 、实现开发需求

		class Emp {
			private int empno;
			private String ename;
			private String job;
			private double sal;
			private double comm;
			private Emp mgr ; //描述雇员领导
			private Dept dept;//描述雇员所在部门
			
			public Emp() {}
			public Emp(int empno, String ename, String  job, double sal, double comm) {
				this.empno = empno;
				this.ename = ename;
				this.job = job;
				this.sal = sal;
				this.comm =comm;
			}
			
			public void setMgr(Emp mgr) {
				this.mgr = mgr ;
			}
			
			public Emp getMgr() {
				return this.mgr;
			}
			public void setDept(Dept dept) {
				this.dept = dept ;
			}
			public Dept getDept() {
				return this.dept;
			}
			public String getInfo() {
				return "【EMP】 empno = " + this.empno + ", ename = " + this.ename +
						", job = " + this.job + ", sal = " + this.sal + ", comm  = "+ this.comm ;
			}
			
		}
		
		class Dept {
			private int deptno;
			private String dname;
			private String loc;
			private Emp [] emps;
			
			public Dept() {}
			public Dept(int deptno, String dname, String loc) {
				this.deptno = deptno;
				this.dname = dname;
				this.loc = loc;
			}
			public void setEmps(Emp [] emps) {
				this.emps = emps;
			}
			public Emp[] getEmps() {
				return this.emps;
			}
			
			public String getInfo() {
				return "【DEPT】  deptno = " + this.deptno + ", dname = " + this.dname + 
						", loc = " + this.loc ;
			}
		}
		
		public class TestDemo {
			public static void main(String args[]) {
				//第一步： 设置类对象间的关系
				//1、 分别创建各自类的实例化对象
				Dept dept = new Dept(10, "ACCOUNTING", "NEW YORK");
				Emp ea = new Emp(7369, "SMITH", "CLERK", 800.0, 0.0);
				Emp eb = new Emp(7566, "ALLEN", "MANAGE", 2450.0, 0.0);
				Emp ec = new Emp(7839, "KING", "PRESIDENT", 5000.0, 0.0);
				//2、 设置雇员领导的关系
				ea.setMgr(eb);
				eb.setMgr(ec);//ec 没有领导，因为他是president
				//3、 设置雇员和部门的关系
				ea.setDept(dept);
				eb.setDept(dept);
				ec.setDept(dept);
				//4、设置部门和雇员的关系
				dept.setEmps(new Emp[] {ea, eb, ec});
				//第二步进行数据的取得
				//5、 一个部门有多个雇员，并且可以输出一个部门的完整信息（包括雇员信息）；
				System.out.println(dept.getInfo());//输出部门信息
				for(int x = 0 ; x < dept.getEmps().length; x++) {
					System.out.println("\t" + dept.getEmps()[x].getInfo());
					if(dept.getEmps()[x].getMgr() != null) {
						System.out.println("\t\t|-" + dept.getEmps()[x].getMgr().getInfo());
					}
				}
				
				System.out.println("====================================================");
				//6、 可以根据一个雇员找到雇员对应的领导信息和雇员所在部门的信息；
				System.out.println(eb.getInfo());
				if(eb.getMgr() != null) {
					System.out.println("\t|-" + eb.getMgr().getInfo());
				}
				if (eb.getDept() != null) {
					System.out.println("\t|-" + eb.getDept().getInfo());
				}
			}
		}

**console：**

	【DEPT】  deptno = 10, dname = ACCOUNTING, loc = NEW YORK
		【EMP】 empno = 7369, ename = SMITH, job = CLERK, sal = 800.0, comm  = 0.0
			|-【EMP】 empno = 7566, ename = ALLEN, job = MANAGE, sal = 2450.0, comm  = 0.0
		【EMP】 empno = 7566, ename = ALLEN, job = MANAGE, sal = 2450.0, comm  = 0.0
			|-【EMP】 empno = 7839, ename = KING, job = PRESIDENT, sal = 5000.0, comm  = 0.0
		【EMP】 empno = 7839, ename = KING, job = PRESIDENT, sal = 5000.0, comm  = 0.0
	====================================================
	【EMP】 empno = 7566, ename = ALLEN, job = MANAGE, sal = 2450.0, comm  = 0.0
		|-【EMP】 empno = 7839, ename = KING, job = PRESIDENT, sal = 5000.0, comm  = 0.0
		|-【DEPT】  deptno = 10, dname = ACCOUNTING, loc = NEW YORK

这种关系的匹配以及数据的取出操作，是必须掌握的，也是日后开发的基本模式。

## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course41)
