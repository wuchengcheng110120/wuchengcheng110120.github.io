## [上一页](course102)
##  【第15个代码模型】综合案例：反射与简单Java类（单级VO设置实现）

现在所有的操作都是使用TestDemo类调用EmpAction类实现的，而EmpAction类的主要作用是在于定位要操作属性的类型。同时该程序应该符合所有简单java类的开发形式，那么也就意味着必须要设计一个单独的类实现。所以新建一个cn.mldn.util.BeanOperation程序类，这个类来作为操作的发出类。

由于这种Bean的处理操作里面肯定需要被重复的取出对象的信息，所以需要再次准备出两个程序类：StringUtils负责进行字符串的处理操作，毕竟属性的名称需要首字母大写，而后再写一个对象的具体操作（取得对象、设置对象内容）。

**范例** 定义StringUtils的程序类：

	package cn.mldn.util;
	/**
	 * 进行字符串的处理操作
	 * @author Administrator
	 *
	 */
	public class StringUtils {
		private StringUtils() {};
		/**
		 * 首字母大写
		 * @param str 要处理的字符串
		 * @return  返回首字母大写的内容
		 */
		public static String initcap(String str) {
			return str.substring(0,1).toUpperCase() + str.substring(1);
		}
	}

**范例** 定义ObjectUtils程序类：

	package cn.mldn.util;
	
	import java.lang.reflect.Field;
	import java.lang.reflect.Method;
	
	/**
	 * 本类的主要功能是根据属性名称调用相应类中的getter和setter方法
	 * @author Administrator
	 *
	 */
	public class ObjectUtils {
		private ObjectUtils() {}
		/**
		 * 根据指定的类对象设置指定类中的属性，调用setter方法
		 * @param warpobject 属性所在类的实例化对象
		 * @param attribute 属性名称
		 */
		public static void setObjectValue(Object warpobject,String attribute,String value) throws Exception{
			Field field = warpobject.getClass().getDeclaredField(attribute);
			if (field == null) {//第二次取得，某些属性通过父类取得
				field = warpobject.getClass().getField(attribute);
			}
			if (field == null) {//以上两次操作都无法取得成员对象
				return ;//该属性一定不存在
			}
			String methodName = "set" + StringUtils.initcap(attribute);//定义方法名称
			Method method = warpobject.getClass().getMethod(methodName, field.getType());
			method.invoke(warpobject, value);
		}
		/**
		 * 负责调用类中的getter方法
		 * @param warpobject 表示要调用的方法的所在类对象
		 * @param attribute 表示属性名称
		 * @return 调用对象的结果
		 */
		public static Object getObject(Object warpobject,String attribute)throws Exception {
			String methodName = "get" + StringUtils.initcap(attribute);//定义方法名称
			// 调用指定属性的Field对象，目的是取得对象类型，如果没有此属性也就意味着该操作无法继续
			Field field = warpobject.getClass().getDeclaredField(attribute);
			if (field == null) {//第二次取得，某些属性通过父类取得
				field = warpobject.getClass().getField(attribute);
			}
			if (field == null) {//以上两次操作都无法取得成员对象
				return null;//该属性一定不存在
			}
			Method method = warpobject.getClass().getMethod(methodName);
			return method.invoke(warpobject);
		}
	}

所有的操作为了保持统一都使用BeanOperation类负责设置。

**范例** 定义BeanOperation：

	package cn.mldn.util;
	
	import java.lang.reflect.Field;
	import java.util.Arrays;
	
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
				String fields [] = attribute.split("\\.");
				Object currentObject = ObjectUtils.getObject(actionObject,fields[0]);
				ObjectUtils.setObjectValue(currentObject, fields[1], value);
			}
		}
	}

下面给出这些类的操作关系：

![](http://ww3.sinaimg.cn/large/0060lm7Tly1fo4fyi2iqpj30lx0b478l.jpg)


## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course104)
