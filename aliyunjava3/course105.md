## [上一页](course104)
##  【第15个代码模型】综合案例：反射与简单Java类（设置各种数据类型）

在实际开发过程中使用最多的几种数据类型：int、double、long、Date、String。所以如果针对于属性类型的处理，也可以只考虑以上几种类型。

**范例** 修改Emp.java类：

	public class Emp {
		private String ename;
		private String job;
		private Double salary;
		private Date hiredate;
		private Dept dept = new Dept();
	}

**范例** 修改Dept.java类：

	public class Dept {
		private String dname;
		private String loc;
		private Long count; //总员工数
		private Company company = new Company();
	}

**范例** 修改Company.java类：

	public class Company {
		private Integer cid;
		private String name;
		private String address;
		private java.util.Date create;
	}

现在程序所支持的数据类型都是在开发中可能出现的内容了。

如果考虑各种数据的情况，很明显不能够使用String来进行内容的设计了，必须考虑使用Object类型。

	public static void setObjectValue(Object warpobject,String attribute,Object value) throws Exception{}
那么也就意味着BeanOperation程序类里面，不能单单再以String作为数值保存了，可能是各种类型，类型需要靠传入对象和属性类型来判断，为了方便处理，再建立一个程序类负责程序的转型，而且所有的转型结果都按照Object处理。

**范例** 定义cn.mldn.util.ObjectValueUtils

	package cn.mldn.util;
	
	import java.lang.reflect.Field;
	import java.text.ParseException;
	import java.text.SimpleDateFormat;
	
	/**
	 * 本类的功能是将字符串的内容根据属性对应的类型变为各种数据类型
	 * 支持的类型有int（Integer）、double（Double）、long（Long）、string（String）
	 * Date、其中Date必须考虑到支持日期时间（yyyy-MM-dd HH-mm-ss），日期（yyyy-MM-dd）
	 * @author Administrator
	 *
	 */
	public class ObjectValueUtils {
		private ObjectValueUtils() {}
		/**
		 * 负责将传入的字符串变为与指定数据类型相符合的数据类型
		 * @param warpObject 要操作的对象
		 * @param attribute 属性类型
		 * @param value 传入的数据（都是字符串）
		 * @return 根据属性类型进行转型处理
		 */
		public static Object getValue(Object warpObject, String attribute,String value)throws Exception {
			Field field = ObjectUtils.getObjectField(warpObject, attribute);
			if (field == null) {
				return null;
			}
			return stringToType(field.getType().getSimpleName(), value);
		}
		/**
		 * 根据指定的类型将字符串进行转型处理
		 * @param type 数据类型
		 * @param value 数据内容
		 * @return 转换为的具体类型
		 */
		private static Object stringToType(String type, String value) {
			if ("String".equals(type)) {//是字符串类型
				if (isNotEmpty(value)) {
					return value;
				}else {
					return null;
				}
			}else if ("int".equals(type)|| "Integer".equals(type)) {
				if (isInt(value)) {//是个整型数据
					return Integer.parseInt(value);
				}
			}else if ("double".equals(type)|| "Double".equals(type)) {
				if (isDouble(value)) {//是个整型数据
					return Double.parseDouble(value);
				}
			}else if ("long".equals(type)|| "Long".equals(type)) {
				if (isInt(value)) {//是个整型数据
					return Long.parseLong(value);
				}
			}else if ("Date".equals(value)) {
				String pattern = null;
				if (isDate(value)) {//是日期型
					pattern = "yyyy-MM-dd";
				}else if (isDateTime(value)) {
					pattern = "yyyy-MM-dd HH-mm-ss";
				}
				if (pattern != null) {
					try {
						return new SimpleDateFormat(pattern).parse(value);
					} catch (ParseException e) {
						e.printStackTrace();
					}
				}else {
					return null;
				}
			}
			return null;
		}
		/**
		 * 判断给定的字符串是否是日期类型（yyyy-MM-dd）
		 * @param str 要判断的字符串
		 * @return 如果是日期格式返回true，否则返回false
		 */
		private static boolean isDate(String str) {
			if (isNotEmpty(str)) {
				return str.matches("\\d{4}-\\d{2}-\\d{2}");
			}
			return false;
		}/**
		 * 判断给定的字符串是否是日期时间类型（yyyy-MM-dd HH-mm-ss）
		 * @param str 要判断的字符串
		 * @return 如果是日期格式返回true，否则返回false
		 */
		private static boolean isDateTime(String str) {
			if (isNotEmpty(str)) {
				return str.matches("\\d{4}-\\d{2}-\\d{2} \\d{2}-\\d{2}\\d{2}");
			}
			return false;
		}
		/**
		 * 判断给定的字符串是否包含双精度小数
		 * @param str 给定的字符串
		 * @return 字符串由小数组成（11,11.0），返回true，否则返回false
		 */
		private static boolean isDouble(String str) {
			if (isNotEmpty(str)) {
				return str.matches("\\d+(\\.\\d+)?");
			}
			return false;
		}
		/**
		 * 判断给定字符串是不是整型
		 * @param str 给定字符串
		 * @return 如果字符串是由整数所组成，就返回true，否则就返回false
		 */
		private static boolean isInt(String str) {
			if (isNotEmpty(str)) {//保证传入的字符串有内容
				return str.matches("\\d+");
			}
			return false;
		}
		/**
		 * 判断字符串是否不是空字符串后才可以进行处理
		 * @param str 要判断的字符串
		 * @return 如果字符串为空，那么返回false，否则返回true
		 */
		private static boolean isNotEmpty(String str) {
			return !(str == null || str.isEmpty() || "".equals(str));
		}
		
	}

**范例** 修改了ObjectUtils.java程序类

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
		 * 根据对象和指定的属性名称取得Field对象信息
		 * @param warpObject 当前操作对象
		 * @param attribute 属性
		 * @return 属性的对象，如果该属性不存在返回null
		 */
		public static Field getObjectField(Object warpObject,String attribute) throws Exception {
			Field field = warpObject.getClass().getDeclaredField(attribute);
			if (field == null) {//第二次取得，某些属性通过父类取得
				field = warpObject.getClass().getField(attribute);
			}
			return field;
		}
		/**
		 * 根据指定的类对象设置指定类中的属性，调用setter方法
		 * @param warpObject 属性所在类的实例化对象
		 * @param attribute 属性名称
		 */
		public static void setObjectValue(Object warpObject,String attribute,Object value) throws Exception{
			Field field = getObjectField(warpObject, attribute);
			if (field == null) {//以上两次操作都无法取得成员对象
				return ;//该属性一定不存在
			}
			String methodName = "set" + StringUtils.initcap(attribute);//定义方法名称
			Method method = warpObject.getClass().getMethod(methodName, field.getType());
			method.invoke(warpObject, value);
		}
		/**
		 * 负责调用类中的getter方法
		 * @param warpObject 表示要调用的方法的所在类对象
		 * @param attribute 表示属性名称
		 * @return 调用对象的结果
		 */
		public static Object getObject(Object warpObject,String attribute)throws Exception {
			String methodName = "get" + StringUtils.initcap(attribute);//定义方法名称
			// 调用指定属性的Field对象，目的是取得对象类型，如果没有此属性也就意味着该操作无法继续
			Field field = getObjectField(warpObject, attribute);
			if (field == null) {//以上两次操作都无法取得成员对象
				return null;//该属性一定不存在
			}
			Method method = warpObject.getClass().getMethod(methodName);
			return method.invoke(warpObject);
		}
	}

**范例** 修改BeanOperation程序类：

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
				//通过拆分属性就可以判断出是单级还是多级
				String fields [] = attribute.split("\\.");
				if (fields.length > 2) {//多级配置
					//如果想要通过多级确定出属性的操作对象，那么就应该一层层的找出每一个getter方法返回的内容
					Object currentObject = actionObject;
					for (int y = 0; y < fields.length - 1; y++) {// 对应的getter的返回对象
						currentObject = ObjectUtils.getObject(currentObject, fields[y]);
					}
					Object value = ObjectValueUtils.getValue(currentObject, fields[fields.length - 1], temp[1]);
					ObjectUtils.setObjectValue(currentObject,fields[fields.length - 1], value);
				}else {//单级配置
					Object value = ObjectValueUtils.getValue(actionObject, attribute, temp[1]);
					Object currentObject = ObjectUtils.getObject(actionObject,fields[0]);
					ObjectUtils.setObjectValue(currentObject, fields[1], value);
				}
			}
		}
	}

随后通过测试的程序类进行内容的设置：

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
				String temp[] = result[x].split(":"，2);
				String attribute  = temp[0]; //属性名称，包括了“XxxAction属性和简单java类的属性”
				//通过拆分属性就可以判断出是单级还是多级
				String fields [] = attribute.split("\\.");
				if (fields.length > 2) {//多级配置
					//如果想要通过多级确定出属性的操作对象，那么就应该一层层的找出每一个getter方法返回的内容
					Object currentObject = actionObject;
					for (int y = 0; y < fields.length - 1; y++) {// 对应的getter的返回对象
						currentObject = ObjectUtils.getObject(currentObject, fields[y]);
					}
					Object value = ObjectValueUtils.getValue(currentObject, fields[fields.length - 1], temp[1]);
					ObjectUtils.setObjectValue(currentObject,fields[fields.length - 1], value);
				}else {//单级配置
					Object currentObject = ObjectUtils.getObject(actionObject,fields[0]);
					Object value = ObjectValueUtils.getValue(currentObject, fields[1], temp[1]);
					ObjectUtils.setObjectValue(currentObject, fields[1], value);
				}
			}
		}
	}
**console：**

	Emp [ename=smith, job=clerk, salary=1999.12, hiredate=Sun Oct 10 00:00:00 CST 1999, dept=Dept [dname=财务部, loc=null, count=892392390, company=Company [cid=10, name=MLDN, address=北京天安门, create=Sat Sep 15 10:10:10 CDT 1990]]]


写代码必须考虑到可重用设计，重复的编码开发必须养成排除的习惯
对于日期时间的的数据由于其字符串中也存在“：”，所以根据冒号的来的拆分的结果是null，为了解决这个问题：手工进行截取
	
	public class TestSpilt {
		public static void main(String[] args) {
			String str = "emp.dept.company.create:1990-09-15 10:10:10";
			String result [] = str.split(":",2);
			for (int x = 0; x < result.length; x++) {
				System.out.println(result[x]);
			}
		}
	}
**console：**

	emp.dept.company.create
	1990-09-15 10:10:10






## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course106)
