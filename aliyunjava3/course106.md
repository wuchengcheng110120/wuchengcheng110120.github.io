## [上一页](course105)
##  【第15个代码模型】综合案例：反射与简单Java类（级联实例化对象）

本程序开发之中最大的败笔实际上就出现在于类之间必须明确实例化好对象的行为，因为用户在操作时很有可能忘记实例化对象，所以为了保证程序依然可以正确执行，当发现用户没有实例化关联类对象时自动实例化，如果已经实例化则保持与之前同样的操作。

**范例** 修改ObjectUtils.java程序类

	public static Object getObject(Object warpObject,String attribute)throws Exception {
		String methodName = "get" + StringUtils.initcap(attribute);//定义方法名称
		// 调用指定属性的Field对象，目的是取得对象类型，如果没有此属性也就意味着该操作无法继续
		Field field = getObjectField(warpObject, attribute);
		if (field == null) {//以上两次操作都无法取得成员对象
			return null;//该属性一定不存在
		}
		Method method = warpObject.getClass().getMethod(methodName);
		Object obj = method.invoke(warpObject);//调用getter返回实例化对象
		if (obj == null) {//现在没有实例化关联类对象，必须自己手工实例化对象
			//所有的程序类都可以通过反射来进行对象的实例化处理，也就是说只需要取得类的对象的类型就可以实现该功能了
			obj  = field.getType().newInstance();
			setObjectValue(warpObject, attribute, obj);
		}
		return obj ;
	}

随着开发经验的积累，应该学会开发一些可以重复使用的工具类，这些工具类主要应用反射来实现。而且工具类应该不断完善。


## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course107)
