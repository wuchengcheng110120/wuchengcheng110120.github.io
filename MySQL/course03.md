
## [上一页](course02)
## 添加和删除数据表

创建数据表table

	create table table_name(
		column_name data_type,
		column_name data_type,
		.
		.
		.
		column_name data_type
	
	);

例子：

	CREATE TABLE account(
		id bigint(20),
		createTime datetime,
		ip varchar(255),
		mobile varchar(255),
		nickname varchar(255),
		passwd varchar(255),
		username varchar(255),
		avatar varchar(255),
		brief text,
		job varchar(255),
		location varchar(255),
		qq varchar(255),
		gender int(11),
		city varchar(255),
		province varchar(255)
	);

删除数据表table

	drop table table_name;

例子：

	show databases;
	create database gc;
	use gc     //Database changed
	show tables;  //Empty set
	
	CREATE TABLE account1(
		id bigint(20),
		createTime datetime,
		ip varchar(255),
		mobile varchar(255),
		nickname varchar(255),
		passwd varchar(255),
		username varchar(255),
		avatar varchar(255),
		brief text,
		job varchar(255),
		location varchar(255),
		qq varchar(255),
		gender int(11),
		city varchar(255),
		province varchar(255)
	);
	describe account;
![](http://ww4.sinaimg.cn/large/0060lm7Tly1fna7iu47eaj30es09lmx6.jpg)

	drop table account1;


## [返回目录](https://wuchengcheng110120.github.io/MySQL/learnMySQL)
## [下一页](course04)
