## [上一页](course103)
##  【第15个代码模型】综合案例：反射与简单Java类（多级VO设置实现）

现在假设一个雇员属于一个部门，一个部门属于一个公司，一个公司属于一个城市，一个城市属于一个省份，一个省份属于一个国家，这种类似的关系都可以通过字符串的配置来实现设置。

**范例** 建立一个Company关系：

	package cn.mldn.vo;
	public class Company {
		private String name;
		private String address;
	}
**范例** 修改Dept类定义：

	package cn.mldn.vo;
	
	public class Dept {
		private String dname;
		private String loc;
		private Company company = new Company();
	}

**范例** 修改Emp类：

	package cn.mldn.vo;
	
	public class Emp {
		private String ename;
		private String job;
		private Dept dept = new Dept();
	}

此时所有的引用关系上都自动进行了实例化。而现在对于程序希望可以满足单级也可以满足无限多级，对于内容的设置可能采用如下代码的实现方式：

**范例** 定义TestEmpDemo的主类：

	package cn.mldn.demo;
	
	import cn.mldn.action.EmpAction;
	
	public class TestEmpDemo {
		public static void main(String[] args) throws Exception {
			String value = "emp.ename:smith|emp.job:clerk|"
					+ "emp.dept.dname:财务部|emp.dept.company.name：MLDN";
			EmpAction action = new EmpAction();
			action.setValue(value);
			System.out.println(action.getEmp());
		} 
	}

![](http://ww1.sinaimg.cn/large/0060lm7Tly1fo4gm8pd9vj30v80hjdl1.jpg)

**范例** 修改BeanOperation中的内容设置方法：

	package cn.mldn.util;
	
	import java.lang.reflect.Field;
	
	/**
	 * 本类主要负责实现自动的VO匹配处理操作，本身不需要通过实例化对象完成，所以构造方法私有化
	 * @author Administrator
	 *
	 */
	public class BeanOperation {
		private BeanOperation(){}
		/**
		 * 负责设置类中的属性操作
		 * @param actionObject 表示当前发出设置请求的程序类的当前对象
		 * @param msg 所有属性的具体内容，格式“属性名称：内容|属性名称：内容|...”
		 */
		public static void setBeanValue(Object actionObject, String msg) throws Exception{
			//如果要进行内容设置，必须进行字符串拆分（此处不关心验证）
			String result[] = msg.split("\\|");//按照竖线进行拆分，取出所有需要设置的内容
		//	System.out.println("**********" + Arrays.toString(result) );
			for (int x = 0; x < result.length; x++) {//此时每次执行后只剩下属性名称和属性内容了
				//需要针对给定的属性名称和内容进行拆分
				String temp[] = result[x].split(":");
				String attribute  = temp[0]; //属性名称，包括了“XxxAction属性和简单java类的属性”
				String value = temp[1]; // 接收具体的属性内容
				//通过拆分属性就可以判断出是单级还是多级
				String fields [] = attribute.split("\\.");
				if (fields.length > 2) {//多级配置
					//如果想要通过多级确定出属性的操作对象，那么就应该一层层的找出每一个getter方法返回的内容
					Object currentObject = actionObject;
					for (int y = 0; y < fields.length - 1; y++) {// 对应的getter的返回对象
						currentObject = ObjectUtils.getObject(currentObject, fields[y]);
					}
					ObjectUtils.setObjectValue(currentObject,fields[fields.length - 1], value);
				}else {//单级配置
					Object currentObject = ObjectUtils.getObject(actionObject,fields[0]);
					ObjectUtils.setObjectValue(currentObject, fields[1], value);
				}
			}
		}
	}
**console：**

	Emp [name=smith, job=clerk]Dept [dname=财务部, loc=null]Company [name=MLDN, address=北京天安门]

这样的程序才可以正常使用，属于多级设置。



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course105)
