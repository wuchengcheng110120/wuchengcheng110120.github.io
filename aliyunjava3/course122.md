## [上一页](course121)
##  使用Statement操作数据库（Statement执行更新操作）

数据更新一共分为三种操作：增加、修改、删除，如果要更新的操作使用的是Statement接口的话，只需要按照结构拼凑出完整的SQL语句即可。

1、 实现数据增加处理

- SQL语法： INSERT INTO 表名称 （字段，字段，...） VALUES(值，值，...)；

		package cn.mldn.demo;
		
		import java.sql.Connection;
		import java.sql.DriverManager;
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
				String sql = " INSERT INTO member(mid,name,age,birthday,note) VALUES "
						+ " (myseq.nextval,'张三',10,SYSDATE,'是个人') " ;
				int len = stmt.executeUpdate(sql);
				System.out.println("数据库更新行数： " + len);
				conn.close();
			}
		}

2、 修改数据

- 修改的SQL： UPDATE 表名称 SET 字段=值，字段=值，字段=值， WHERE 更新条件；

		package cn.mldn.demo;
		
		import java.sql.Connection;
		import java.sql.DriverManager;
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
				String sql = " UPDATE member SET name='李四',age=20 WHERE mid IN (1,2) " ;
				int len = stmt.executeUpdate(sql);
				System.out.println("数据库更新行数： " + len);
				conn.close();
			}
		}

**范例** 删除数据：

	package cn.mldn.demo;
	
	import java.sql.Connection;
	import java.sql.DriverManager;
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
			String sql = " DELETE FROM member WHERE mid BETWEEN 1 AND 2 " ;
			int len = stmt.executeUpdate(sql);
			System.out.println("数据库更新行数： " + len);
			conn.close();
		}
	}

通过以上的执行也可以发现一些规律：使用Statement进行数据库操作的时候，直接编写一个数据库可以读懂的sql语句即可。



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course123)
