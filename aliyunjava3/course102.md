## [上一页](course101)
##  【第15个代码模型】综合案例：反射与简单Java类（单极VO操作原理）

以后所有的项目开发中都会有反射的应用，到最后使用的所有框架里面到处都是反射的身影，没有反射就没有开发框架，没有反射框架的存在意义就没有了。下面将主要结合简单java类来进行反射开发的深入研究，同时这些也是SpringMVC、Struts开发框架的主要操作原理。

现在有一个简单java类，这个简单java类中的属性按照原始的做法一定要通过setter才可以设置，取得使用getter（不关注此处）。

**范例** 基本程序：

	package cn.mldn.vo;
	
	public class Emp {
		private String name;
		private String job;
		public String getName() {
			return name;
		}
		public void setName(String name) {
			this.name = name;
		}
		public String getJob() {
			return job;
		}
		public void setJob(String job) {
			this.job = job;
		}
	}

现在Emp中存在有无参构造方法，于是下面如果按照传统调用，则编写如下：

	package cn.mldn.demo;
	
	import cn.mldn.vo.Emp;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			Emp vo = new Emp();
			vo.setName("SMITH");
			vo.setJob("CLERK");
			System.out.println(vo);
		} 
	}
**console：**

	Emp [name=SMITH, job=CLERK]

但是这个时候觉得这个操作太麻烦了，假设一个类中存在几十个属性，那么要写几十次的setter方法，现在希望可以简化一些，例如：给定一个字符串，格式“属性名称：内容|属性名称：内容|...”，能够按照这样的形式将内容全部设置到属性里面。

![](http://ww3.sinaimg.cn/large/0060lm7Tly1fo4aax3552j30vf0hf46i.jpg)

通过本程序想要实现实现任意的简单java类的属性设置。


## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course103)
