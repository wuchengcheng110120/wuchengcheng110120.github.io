## [上一页](course09)
## 使用order by 对查询结果排序

### order by

1、 按单一列名排序：

select * from table_name [where子句] order by col_name[asc/desc]

2、 按多列排序：

select * from table_name [where子句] order by col1[asc/desc], col2[asc/desc]...

不加asc/desc时， 默认为asc


增加一列数据pages：

alter table book add pages int；

修改某一数据：update 【table_name】set 【col1_name】 = 值 where【col2_name】 = 值

update book set id = 2 where id is null and title = 'title1';

update book set id = 5 where id is null and title is null；

![](http://ww2.sinaimg.cn/large/0060lm7Tly1fnacuwsm03j30fn0aeaa0.jpg)




## [返回目录](https://wuchengcheng110120.github.io/MySQL/learnMySQL)
## [下一页](course11)
