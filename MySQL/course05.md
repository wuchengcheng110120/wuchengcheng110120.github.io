## [上一页](course04)
## 修改table-修改列信息和表名

### 修改列信息

alter table 【table_name】 change 【old_column_name】【new_column_name】

【data_type】

1、 只改列名：

data_type 和原来一样， old_column_name != new_column_name

2、 只改数据类型：

old_column_name == new_column_name, data_type改变

3、列名和数据类型都改了


### 修改表名 

alter table 【table_name】 rename 【new_table_name】

例子：

alter table account rename newaccount；








## [返回目录](https://wuchengcheng110120.github.io/MySQL/learnMySQL)
## [下一页](course06)
