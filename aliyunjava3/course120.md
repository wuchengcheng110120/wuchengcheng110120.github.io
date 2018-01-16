## [上一页](course119)
## 连接Oracle数据库

如果要进行数据库的处理操作，首先要做的就是连接，但是如果要想正确的连接数据库，就必须有数据库的驱动程序，Oracle数据库的驱动程序都会自动的安装在目标路径（我使用的是mysql）：

使用命令行直接编辑环境的CLASSPATH属性即可，如果使用Eclipse的话则必须修改“Java Build Path”进行扩展开发包的引用。（导入jar包mysql-connector-java-5.1.44-bin）如果不配置会出现“ClassNotFindException”

但是千万要记住一点，如果要想使用Oracle操作请保证服务打开：

- 监听服务 ；

- 实例服务


如果要想进行数据库的连接在JDBC之中使用java.sql.Connection接口描述的是每一个数据库的连接信息，也就是说如果一个用户操作时，那么只要获得了Connection接口的对象就可以操作数据库。

但是如果想要取得Connection的接口对象，则需要使用java.sql.DriverManager的程序类；

- 取得连接方法： public static Connection getConnection(String url,
                                       String user,
                                       String password)
                                throws SQLException

返回一个java.sql.Connection 接口；

但是如果想要进行数据库的连接操作则需要以下四个信息：jdbc:oracle:thin:@localhost:1521:orcl

- 数据库驱动程序： lib中连接jar包后导入：oracle.jdbc.driver.OracleDriver

- 连接地址 url：不同的数据库有不同的连接地址

	|- Oracle 连接格式：jdbc:oracle:thin:@主机名称:端口:数据库实例名称（SID）：

		|- 连接Orcl：jdbc:oracle:thin:@localhost:1521:orcl

- 用户名： scott；

- 密码： tiger；

下面就可以给出JDBC的具体的操作步骤：

- 向容器之中进行数据库驱动的加载： Class.forName(数据库驱动程序)：
		
	Class.forName(oracle.jdbc.driver.OracleDriver);

- 通过DriverManager取得一个连接对象：DriverManager.getConnection()

- 通过连接对象创建所有的数据库操作对象，并且进行数据库的更新、查询

- 数据库属于资源操作，资源操作的结束必须关闭（close()）


**范例** 实现数据库的连接

	package cn.mldn.demo;
	
	import java.sql.Connection;
	import java.sql.DriverManager;
	
	public class TestJDBCDemo {
		public static final String DBDRIVER = "oracle.jdbc.driver.OracleDriver";
		public static final String DBURL = "jdbc:oracle:thin:@localhost:1521:orcl";
		public static final String DBUSER = "scott";
		public static final String DBPASSWORD = "tiger";
		public static void main(String[] args) throws Exception{
			Class.forName(DBDRIVER);//进行数据库驱动的加载
			Connection conn = DriverManager.getConnection(DBURL, DBUSER, DBPASSWORD);
			System.out.println(conn);
			conn.close();
		}
	}

**console：**

	oracle.jdbc.driver.T4CConnection@cd51c3

说明： 关于Oracle连接不上的问题

1、环境属性改变：你现在修改了你的主机名称，所以无法进行数据库的连接；

- 此时需要修改Oracle中的环境配置文件：F:\oracle\product\10.2.0\db_1\NETWORK\ADMIN；

- 该目录有两个文件：listener.ora、tnsnames.ora，是相关连接设置

	
2、 当你的环境出现了问题之后，那么有可能你之前配置的SID就丢失了，那么在进行连接的时候就会出现	
找不到SID

这个时候需要自己去注册这个SID，这个时候可以利用Oracle给出的一个图形化界面进行修改（Net Manager）listener中添加数据库；

数据库连接完成后，分析程序采用的模式：工厂设计模式，DriverManager就是一个工厂类；

![](http://ww1.sinaimg.cn/large/0060lm7Tly1fnic9vowiuj30vi0hcqbr.jpg)

以后你的工作之中可能连接各种数据库，但是千万要记住，不管连接什么数据库，由于工厂设计模式的使用，我们关心的只是接口和工厂类（DriverManager和Connection）




## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course121)
