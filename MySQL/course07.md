## [上一页](course06)
## where条件查询

### where语法

select * from table_name where col_name 运算符 值

例子：

select * from book where title = 't';

![](http://ww1.sinaimg.cn/large/0060lm7Tly1fnaaf5xxsjj30oo0ffact.jpg)

组合条件 and、or

where后面可以通过and与or运算符组合多个条件筛选

语法：

select * from table_name where col1 = xxx and col2 = xx or col3 > xx

select * from book where id = 1;

select * from book where id = 1 or content = 'c';

select * from book where id = 3 and (content = 'c' or title = 't');






## [返回目录](https://wuchengcheng110120.github.io/MySQL/learnMySQL)
## [下一页](course08)
