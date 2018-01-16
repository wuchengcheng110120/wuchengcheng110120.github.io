## [上一页](course000）
## SQLPLUS命令

Oracle安装完成之后会自动提供一个sqlplus命令，直接运行此命令即可。输入用户名和密码（密码不回显）。

除了此种方式之外，也可以直接启用命令行模式运行cmd，输入命令：

	sqlplus scott/tiger 

数据库基本组成是数据表，每一张表会包含有多条数据记录，下面查询一下emp 表的数据

	select * from emp;
“/”： 表示执行语句；

现在执行之后显示的格式是比较混乱的，混乱的原因是因为此时没有设置环境：

- 设置每行显示数据的长度： SET LINESIZE 300 ;(命令不区分大小写)

		|- 因为此显示会受到命令行的限制

- 设置每页显示的数据行数： SET PAGESIZE 30;

这两个命令称为格式化指令。

windows系统下命令编辑很方便，但是很多的Oracle运行的时候都是没有图形界面的，所以一般这样的情况下，要想编写程序代码就必须启动本地的记事本程序；

输入命令“ed 文件名称”（如果不写后缀，默认的后缀就是*.sql）输入 ed mldn

打开记事本之后就相当于进入了程序阻塞状态，必须等记事本关闭之后才可以继续使用，随后要向执行文件中的命令，那么使用“@文件名称”，默认找到*.sql的后缀

在Oracle里面提供四个用户，可以在sqlplus中使用以下语法切换用户：

CONN 用户名/密码  [AS SYSDBA]

如果现在使用的是sys用户登录，那么必须要写上“AS SYSDBA”,否则无法登陆；

**范例** 使用system登陆：

	conn system/root


**范例** 使用sys登陆：

	conn sys/root as sysdba

select * from emp;

emp表属于scott用户，在sys用户下不存在；

表的完全名称“用户名.表名称”，即scott.emp。

**范例** 使用完整名称访问

	select * from scott.emp;

在sqlplus中除了可以使用Oracle自己定义的命令外，也可以利用HOST指令调用本机的操作系统命令；

**范例** 调用echo命令

host echo helloworld

**范例** 调用copy命令

host copy 源文件路径 拷贝路径


1、 格式化命令：

- 设置每行的长度： SET LINESIZE 长度；

- 设置每页的长度： SET PAGESIZE 长度；

2、 切换用户 ：

- CONN 用户名/密码 [AS SYSDBA], 如果是sys用户一定要写上[AS SYSDBA]

3、 调用本机命令 : HOST 作为前缀；



## [返回目录](https://wuchengcheng110120.github.io/Oracle/list)
## [下一页](course02)
