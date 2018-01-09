## [上一页](course03)
## 修改table - 增删列

### 增加列

alter table 【table_name】 add 【colunm_name】【data_type】

[not null][default]

例子： 
 
alter table account add c1 int(11) not null default 1;

describe account;

![](http://ww1.sinaimg.cn/large/0060lm7Tly1fna7vwi0noj30em0apmx8.jpg)

### 删除列

alter table 【table_name】 drop 【column_name】

例子：

alter table account drop c1;




## [返回目录](https://wuchengcheng110120.github.io/MySQL/learnMySQL)
## [下一页](course05)
