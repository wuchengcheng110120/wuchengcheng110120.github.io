## [上一页](course124)
##  使用PreparedStatement操作数据库（PreparedStatement查询案例）

由于在实际开发之中PreparedStatement的使用频率非常的高，所以对于此接口的查询操作就特别重要。下面列出几个最为基础的查询处理模型，这些基本的案例编写熟练之后就可以编写程序了。

1、查询全部：

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
			Class.forName(DBDRIVER);//进行数据库驱动的加载
			Connection conn = DriverManager.getConnection(DBURL, DBUSER, DBPASSWORD);
			Statement stmt = conn.createStatement(); // 创建数据库操作对象
			String sql = " SELECT mid,name,age,birthday,note FROM member " ;
			PreparedStatement  pstmt = conn.prepareStatement(sql);
			ResultSet rs = pstmt.executeQuery();
			while (rs.next()) {
				int mid = rs.getInt(1);
				String name = rs.getString(2);
				int age = rs.getInt(3);
				Date birthday = rs.getDate(4);
				String note = rs.getString(5);
				System.out.println(mid + "、" + name + "、" + age + "、" + birthday + "、" + note);
			}
			conn.close();
		}
	}

**console：**

	1、张三、10、2018-02-11、是个人
	2、李四、20、2018-02-11、是个人
	3、李四、20、2018-02-11、是个人
	4、李四、20、2018-02-11、是个人
	21、王五、18、1989-10-10、不错，是个人！
	22、Mr'Smith、18、2018-02-11、不错，是个人！
	

2、 进行根据id查询：

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
			Class.forName(DBDRIVER);//进行数据库驱动的加载
			Connection conn = DriverManager.getConnection(DBURL, DBUSER, DBPASSWORD);
			Statement stmt = conn.createStatement(); // 创建数据库操作对象
			String sql = " SELECT mid,name,age,birthday,note FROM member " ;
			PreparedStatement  pstmt = conn.prepareStatement(sql);
			ResultSet rs = pstmt.executeQuery();
			while (rs.next()) {
				int mid = rs.getInt(1);
				String name = rs.getString(2);
				int age = rs.getInt(3);
				Date birthday = rs.getDate(4);
				String note = rs.getString(5);
				System.out.println(mid + "、" + name + "、" + age + "、" + birthday + "、" + note);
			}
			conn.close();
		}
	}
**console：**

	21、王五、18、1989-10-10、不错，是个人！

3、 模糊查询处理：

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
			String column = "name";   // 模糊查询所在列
			String keyword = "李" ;  // 关键字
			Class.forName(DBDRIVER);//进行数据库驱动的加载
			Connection conn = DriverManager.getConnection(DBURL, DBUSER, DBPASSWORD);
			Statement stmt = conn.createStatement(); // 创建数据库操作对象
			String sql = " SELECT mid,name,age,birthday,note FROM member WHERE "  + column + " LIKE ? ";
			// 使用？ 填充的占位符只有数据才可以使用，对于列名是无法使用的
			PreparedStatement  pstmt = conn.prepareStatement(sql);
			pstmt.setString(1, "%"+keyword+"%");
			ResultSet rs = pstmt.executeQuery();
			while (rs.next()) {
				int mid = rs.getInt(1);
				String name = rs.getString(2);
				int age = rs.getInt(3);
				Date birthday = rs.getDate(4);
				String note = rs.getString(5);
				System.out.println(mid + "、" + name + "、" + age + "、" + birthday + "、" + note);
			}
			conn.close();
		}
	}

**console：**

	2、李四、20、2018-02-11、是个人
	3、李四、20、2018-02-11、是个人
	4、李四、20、2018-02-11、是个人

4、 分页查询：

	package cn.mldn.demo;
	
	import java.sql.Connection;
	import java.sql.DriverManager;
	import java.sql.PreparedStatement;
	import java.sql.ResultSet;
	import java.sql.Statement;
	import java.util.Date;
	
	import org.junit.jupiter.params.shadow.com.univocity.parsers.common.ColumnMap;
	
	
	public class TestJDBCDemo {
		public static final String DBDRIVER = "oracle.jdbc.driver.OracleDriver";
		public static final String DBURL = "jdbc:oracle:thin:@localhost:1521:orcl";
		public static final String DBUSER = "scott";
		public static final String DBPASSWORD = "tiger";
		public static void main(String[] args) throws Exception{
			int currentPage = 1; //当前在第一页
			int lineSize = 5;	//每页显示5行记录
			String column = "name";   // 模糊查询所在列
			String keyword = "李" ;  // 关键字
			Class.forName(DBDRIVER);//进行数据库驱动的加载
			Connection conn = DriverManager.getConnection(DBURL, DBUSER, DBPASSWORD);
			Statement stmt = conn.createStatement(); // 创建数据库操作对象
			String sql = " SELECT * FROM ("
					+ " SELECT mid,name,age,birthday,note, ROWNUM rn "
					+ " FROM member WHERE " + column + " LIKE ? AND ROWNUM<=?) temp"
							+ " WHERE temp.rn>?  ";
			// 使用？ 填充的占位符只有数据才可以使用，对于列名是无法使用的
			PreparedStatement  pstmt = conn.prepareStatement(sql);
			pstmt.setString(1, "%"+keyword+"%");
			pstmt.setInt(2, currentPage*lineSize);
			pstmt.setInt(3, (currentPage - 1)*lineSize);
			ResultSet rs = pstmt.executeQuery();
			while (rs.next()) {
				int mid = rs.getInt(1);
				String name = rs.getString(2);
				int age = rs.getInt(3);
				Date birthday = rs.getDate(4);
				String note = rs.getString(5);
				System.out.println(mid + "、" + name + "、" + age + "、" + birthday + "、" + note);
			}
			conn.close();
		}
	}

5、 统计查询

	package cn.mldn.demo;
	
	import java.sql.Connection;
	import java.sql.DriverManager;
	import java.sql.PreparedStatement;
	import java.sql.ResultSet;
	import java.sql.Statement;
	import java.util.Date;
	
	import org.junit.jupiter.params.shadow.com.univocity.parsers.common.ColumnMap;
	
	
	public class TestJDBCDemo {
		public static final String DBDRIVER = "oracle.jdbc.driver.OracleDriver";
		public static final String DBURL = "jdbc:oracle:thin:@localhost:1521:orcl";
		public static final String DBUSER = "scott";
		public static final String DBPASSWORD = "tiger";
		public static void main(String[] args) throws Exception{
			String column = "name";   // 模糊查询所在列
			String keyword = "李" ;  // 关键字
			Class.forName(DBDRIVER);//进行数据库驱动的加载
			Connection conn = DriverManager.getConnection(DBURL, DBUSER, DBPASSWORD);
			Statement stmt = conn.createStatement(); // 创建数据库操作对象
			String sql = " SELECT COUNT(*) FROM member WHERE " + column + " LIKE ? ";
			// 使用？ 填充的占位符只有数据才可以使用，对于列名是无法使用的
			PreparedStatement  pstmt = conn.prepareStatement(sql);
			pstmt.setString(1, "%"+keyword+"%");
			ResultSet rs = pstmt.executeQuery();
			if (rs.next()) {
				long count = rs.getLong(1);
				System.out.println(count);
			}
			conn.close();
		}
	}

以上所给出的几个开发代码，是后续开发项目的核心基础部分，需要熟练掌握。

**总结：**

1、 PreparedStatement与Statement相比，其代码的重用设计更难；

2、 PreparedStatement的几个查询将作为以后项目编写的基础。




## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course126)
