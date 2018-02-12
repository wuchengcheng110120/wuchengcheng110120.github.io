## [上一页](course126)
##  批处理与事务处理（事务处理）

事务保证的是所有的更新操作，要么一次成功，要么全部失败，现在对于给定的批处理里面会发现可以一次性的执行多条更新操作，那么假设说中间有一条失败了会如何呢？

**范例** 观察失败的代码：

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
				if (x == 3) {
					stmt.addBatch(" INSERT INTO member(mid,name) VALUES (myseq.nextval,'hello'ni') ");
				}else {
					stmt.addBatch(sql.replaceFirst("#name#", "mldn - " + x));
				}
			}
			int result[] = stmt.executeBatch();
			System.out.println(Arrays.toString(result));
			conn.close();
		}
	}

此时语句的执行出现了错误，结果错误之前的语句正常执行了，而错误之后的语句没有执行，那么如果这些更新属于同一个业务的处理操作，那么此时的数据就乱了。所以为了保证整体的操作要么一起成功，要么一起失败，就可以利用JDBC的原生（数据库）事务进行解决，而事务的控制方法都在Connection接口里面；

- 设置是否自动提交：public void setAutoCommit(boolean autoCommit)
            throws SQLException

- 提交事务： public void commit()
     throws SQLException

- 回滚事务： public void rollback()
       throws SQLException

**范例** 解决事务：

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
			conn.setAutoCommit(false);  // 取消自动提交处理
			try {
				String sql = " INSERT INTO member(mid,name) VALUES (myseq.nextval,'#name#') ";
				// 使用？ 填充的占位符只有数据才可以使用，对于列名是无法使用的
				Statement  stmt = conn.createStatement();
				for (int x = 0; x < 10; x++) {
					if (x == 3) {
						// stmt.addBatch(" INSERT INTO member(mid,name) VALUES (myseq.nextval,'hello'ni') ");
					}else {
						stmt.addBatch(sql.replaceFirst("#name#", "mldn - " + x));
					}
				}
				int result[] = stmt.executeBatch();
				System.out.println(Arrays.toString(result));
				conn.commit(); //真正发出提交
			}catch (Exception e) {
				e.printStackTrace();
				conn.rollback();
			}
			conn.close();
		}
	}

对于事务的操作概念理解即可，因为在以后的开发中这种手工的事务处理并不好用，会有其他的工具来帮助用户自动处理事务。



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course128)
