## [上一页](course125)
##  批处理与事务处理（批处理）

在之前使用的JDBC的操作形式严格来讲都是从JDK1.0开始兴起的，现在的JDBC的版本已经更新到X.0（没人关注）。

现在在使用JDBC时可以发现里面的操作已经优化了不少，例如：最初操作的时候必须按照顺序取，并且只能够取一次。

而从JDBC2.0开始追加了一些神奇的新功能：结果集更新、可滚动结果集、批处理（可以用）；

所谓的批处理指的是多条SQL语句可以同时进行更新处理。而批处理追加之后Statement和PreparedStatement两个接口里面也追加了一些处理方法：

- Statement接口定义的批处理方法：

	|-增加一个待执行SQL:public void addBatch(String sql)
       throws SQLException

	|- 执行批处理 ： public int[] executeBatch()
            throws SQLException

	|- 执行批处理 ： public int[] executeBatch()
            throws SQLException

- PreparedStatement接口定义的批处理方法：

	|- 增加一个待执行SQL: public void addBatch()
       throws SQLException

**范例** 使用PreparedStatement接口实现批处理：

	package cn.mldn.demo;
	
	import java.sql.Connection;
	import java.sql.DriverManager;
	import java.sql.PreparedStatement;
	import java.sql.ResultSet;
	import java.sql.Statement;
	import java.util.Arrays;
	import java.util.Date;
	
	import org.junit.jupiter.params.shadow.com.univocity.parsers.common.ColumnMap;
	
	public class TestJDBCDemo {
		public static final String DBDRIVER = "oracle.jdbc.driver.OracleDriver";
		public static final String DBURL = "jdbc:oracle:thin:@localhost:1521:orcl";
		public static final String DBUSER = "scott";
		public static final String DBPASSWORD = "tiger";
		public static void main(String[] args) throws Exception{
			Class.forName(DBDRIVER);//进行数据库驱动的加载
			Connection conn = DriverManager.getConnection(DBURL, DBUSER, DBPASSWORD);
			Statement stmt = conn.createStatement(); // 创建数据库操作对象
			String sql = " INSERT INTO member(mid,name) VALUES (myseq.nextval,?) ";
			// 使用？ 填充的占位符只有数据才可以使用，对于列名是无法使用的
			PreparedStatement  pstmt = conn.prepareStatement(sql);
			for (int x = 0; x < 10; x++) {
				pstmt.setString(1, "mldn - " + x);
				pstmt.addBatch();  //将操作加入到批处理之中
			}
			int result[] = pstmt.executeBatch();
			System.out.println(Arrays.toString(result));
			conn.close();
		}
	}

**范例** 使用Statement实现批处理：

	package cn.mldn.demo;
	
	import java.sql.Connection;
	import java.sql.DriverManager;
	import java.sql.PreparedStatement;
	import java.sql.ResultSet;
	import java.sql.Statement;
	import java.util.Arrays;
	import java.util.Date;
	
	import org.junit.jupiter.params.shadow.com.univocity.parsers.common.ColumnMap;
	
	
	public class TestJDBCDemo {
		public static final String DBDRIVER = "oracle.jdbc.driver.OracleDriver";
		public static final String DBURL = "jdbc:oracle:thin:@localhost:1521:orcl";
		public static final String DBUSER = "scott";
		public static final String DBPASSWORD = "tiger";
		public static void main(String[] args) throws Exception{
			Class.forName(DBDRIVER);//进行数据库驱动的加载
			Connection conn = DriverManager.getConnection(DBURL, DBUSER, DBPASSWORD);
			String sql = " INSERT INTO member(mid,name) VALUES (myseq.nextval,'#name#') ";
			// 使用？ 填充的占位符只有数据才可以使用，对于列名是无法使用的
			Statement  stmt = conn.createStatement();
			for (int x = 0; x < 10; x++) {
				stmt.addBatch(sql.replaceFirst("#name#", "mldn - " + x));
			}
			int result[] = stmt.executeBatch();
			System.out.println(Arrays.toString(result));
			conn.close();
		}
	}

批处理的特点就是所有的操作一次性的向数据库中发出。


## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course127)
