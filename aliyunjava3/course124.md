## [上一页](course123)
##  使用PreparedStatement操作数据库（Statement执行分析）

在所有的开发项目中不会有人使用Statement，而唯一可以使用的只有PreparedStatement子接口。

Statement在操作上非常的直观，因为只要传入一个完整的sql语句就可以实现相应的数据库操作了。但是这种操作如果真的结合到开发之中是非常混乱的。

**范例** 观察Statement的问题：

	package cn.mldn.demo;
	
	import java.sql.Connection;
	import java.sql.Date;
	import java.sql.DriverManager;
	import java.sql.ResultSet;
	import java.sql.Statement;
	
	
	public class TestJDBCDemo {
		public static final String DBDRIVER = "oracle.jdbc.driver.OracleDriver";
		public static final String DBURL = "jdbc:oracle:thin:@localhost:1521:orcl";
		public static final String DBUSER = "scott";
		public static final String DBPASSWORD = "tiger";
		public static void main(String[] args) throws Exception{
			String name  = "Mr'Smith";
			int age = 18;
			String birthday = "1989-10-10";
			String note = "不错，是个人！";
			Class.forName(DBDRIVER);//进行数据库驱动的加载
			Connection conn = DriverManager.getConnection(DBURL, DBUSER, DBPASSWORD);
			Statement stmt = conn.createStatement(); // 创建数据库操作对象
			String sql = " INSERT INTO member(mid,name,age,birthday,note) VALUES "
					+ " (myseq.nextval,'"+name+"',"+age+",TO_DATE('"+birthday+"','yyyy-MM-dd'),'"+note+"') " ;
			System.out.println(sql);
			int len = stmt.executeUpdate(sql);
			System.out.println("数据库更新行数： " + len);
			conn.close();
		}
	}

**console：**

	INSERT INTO member(mid,name,age,birthday,note) VALUES  (myseq.nextval,'Mr'Smith',18,TO_DATE('1989-10-10','yyyy-MM-dd'),'不错，是个人！') 
	Exception in thread "main" java.sql.SQLException: ORA-00917: 缺失逗号

在SQL中单引号用于描述字符串，所以如果采用了拼凑SQL的语句形式，那么这个符号的处理比较麻烦。另外如果使用Statement处理的时候对于日期的定义非常收到数据库的局限。所以综合的结论就是在开发中不要使用Statement，如果要使用就使用Statement的子接口：PreparedStatement子接口来完成。

如果想要取得本接口的实例化对象，则需要使用Connection接口处理，在Connection接口里面定义有如下方法：

 public PreparedStatement prepareStatement(String sql)
                            throws SQLException

- 这里面的SQL需要使用占位符来描述，而使用“？”作为占位符，编号从1开始。


而取得了PreparedStatement接口对象之后如果要想执行数据库操作，那么也要更换方法：

- 更新操作： public int executeUpdate()
           throws SQLException

- 查询操作： public ResultSet executeQuery()
                throws SQLException

- 填充数据： public void setXxx（int index，数据类型，变量）

在使用PreparedStatement接口操作Date数据的时候特别要引起注意：使用的是java.sql.Date类，而在实际程序之中描述日期Date一定是java.util.Date类，而在java.util.Date中有三个子类：Date（日期）、Time（时间）、Timestamp（日期时间），这三个子类都有一个类似的构造方法：

- java.sql.Date类：public Date(long date)

- java.sql.Time类：public Time(long time)

- java.sql.Timestamp类：public Timestamp(long time)

而在java.util.Date中有一个方法getTime（）可以讲Date变为long。

**范例** 使用PreparedStatement来解决之前的问题：

	package cn.mldn.demo;
	
	import java.sql.Connection;
	import java.sql.DriverManager;
	import java.sql.PreparedStatement;
	import java.sql.ResultSet;
	import java.sql.Statement;
	import java.util.Date;
	
	
	public class TestJDBCDemo {
		public static final String DBDRIVER = "oracle.jdbc.driver.OracleDriver";
		public static final String DBURL = "jdbc:oracle:thin:@localhost:1521:orcl";
		public static final String DBUSER = "scott";
		public static final String DBPASSWORD = "tiger";
		public static void main(String[] args) throws Exception{
			String name  = "Mr'Smith";
			int age = 18;
			Date birthday =new Date();
			String note = "不错，是个人！";
			Class.forName(DBDRIVER);//进行数据库驱动的加载
			Connection conn = DriverManager.getConnection(DBURL, DBUSER, DBPASSWORD);
			Statement stmt = conn.createStatement(); // 创建数据库操作对象
			String sql = " INSERT INTO member(mid,name,age,birthday,note) VALUES "
					+ " (myseq.nextval,?,?,?,?) " ;
			PreparedStatement  pstmt = conn.prepareStatement(sql);
			pstmt.setString(1, name);
			pstmt.setInt(2, age);
			pstmt.setDate(3, new java.sql.Date(birthday.getTime()));
			pstmt.setString(4, note);
			System.out.println("数据库更新行数： " + pstmt.executeUpdate());
			conn.close();
		}
	}

在以后的开发之中不要再去使用Statement处理，都要使用PreparedStatement来处理，如果增加可以实现，修改和删除，同样可以实现。



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course125)
