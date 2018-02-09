## [上一页](course120)
##  使用Statement操作数据库（Statement接口简介）

当取得数据库连接之后所需要进行的就是数据库的操作，而在java.sql包里面，数据库操作的最基础的接口就是Statement接口。但是如果要取得Statement接口对象就必须依靠连接来完成，也就是说要使用Connection接口定义的一个方法：

- 取得Statement接口对象：public Statement createStatement() throws SQLException 当取得了Statement接口之后如果想要进行数据库的操作，则会主要依靠两个方法

- 更新数据库：public int executeUpdate(String sql,String[] columnNames) throws SQLException 返回更新行数；

- 查询数据库：public ResultSet executeQuery(String sql) throws SQLException ；

![](http://ww1.sinaimg.cn/large/0060lm7Tly1fo9io9wqxrj30va0hhgro.jpg)

门面设计模式：一层层接口对象打开。

下面为开发准备出一张数据表：

**范例** 编写数据表创建脚本：

	DROP TABLE member PURUGE;
	DROP SEQUENCE myseq;
	CREATE SEQUENCE myseq;
	CREATE TABLE member (
		mid			NUMBER ,
		name		VARCHAR2(50)	NOT NULL ,
		age			NUMBER ,
		birthday 	DATE ,
		note		CLOB ,
		CONSTRAINT  pk_mid PRIMARY KEY(mid)
	);

sqlplus scott/tiger
select * from tab ;

clear scr ;
select * from tab ;
desc member ;



现在这张数据表里面就包含了所有的常用字段类型



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course122)
