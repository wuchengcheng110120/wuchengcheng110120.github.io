## [上一页](course122)
##  使用Statement操作数据库（Statement执行查询操作）

查询语句指的是向数据库发出我们的查询操作，而后数据库会把满足查询条件的数据返回。数据库把满足条件的数据返回给程序，实际上这些数据就会保存在内存之中，那么如果此时返回的数据量过大，则一定会造成性能的下降，也就是说在查询的时候请考虑到实际的数据量问题。

在Statement接口中如果要进行查询，返回的是一个ResultSet接口对象，那么此接口对象可以包装任意的返回结果（行、列的数据结构）。

![](https://s1.ax1x.com/2018/02/11/9GrLZt.png)

![](https://s1.ax1x.com/2018/02/11/9Gs9Mj.png)

**范例** 实现数据查询：

- 在以后所有的数据库开发过程中，绝对不允许出现“SELECT * ”,出现了会产生问题，写查询语句的时候必须明确的写上具体的数据类型。

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
			Class.forName(DBDRIVER);//进行数据库驱动的加载
			Connection conn = DriverManager.getConnection(DBURL, DBUSER, DBPASSWORD);
			Statement stmt = conn.createStatement(); // 创建数据库操作对象
			String sql = " SELECT mid,name,age,birthday,note FROM member ORDER BY mid " ;
			ResultSet rs = stmt.executeQuery(sql); //查询操作，此时的查询结果都在ResultSet里面
			while(rs.next()) {//有记录就会输出
				int mid = rs.getInt("mid");
				String name = rs.getString("name");
				int age = rs.getInt("age");
				Date birthday = rs.getDate("birthday");
				String note = rs.getString("note");
				System.out.println(mid + "、" + name + "、" + age + "、" + "birthday" + "、" + "note");
			}
			conn.close();
		}
	}

另外以上在取出的时候使用了getXxx（字段名称），这种做法一般不常用，因为在SELECT子句定义的时候已经明确的给出了要使用的字段，所以重复编写没有意义，那么习惯的做法是编写序号。

	while(rs.next()) {//有记录就会输出
				int mid = rs.getInt(1);
				String name = rs.getString(2);
				int age = rs.getInt(3);
				Date birthday = rs.getDate(4);
				String note = rs.getString(5);
				System.out.println(mid + "、" + name + "、" + age + "、" + birthday + "、" + note);
	}

查询的整体的操作流程都是固定流程，取出数据结果集，结果集循环输出。是否使用循环要看使用的数据量来决定。

套路，纯粹的套路，JDBC就是个固定使用的套路，开发中没人用statement；



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course124)
