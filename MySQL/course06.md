## [上一页](course05)
## 查看/插入表数据

查看表数据

select * from table_name;

select col_name ,col_name2,...,from table_name;

插入表数据

insert into 【table_name】 values(值1，值2，...)

insert into 【table_name】 (列1，列2...) values （值1，值2，...）


	create table book(
		id bigint(20),
		title varchar(255),
		content text
	)；

	insert into book values(1, 't hah', 'content');

	insert into book(title) values('title1');


![](http://ww3.sinaimg.cn/large/0060lm7Tly1fnaa1p2tbuj30e008a0sn.jpg)



## [返回目录](https://wuchengcheng110120.github.io/MySQL/learnMySQL)
## [下一页](course07)
