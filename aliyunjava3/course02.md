
## [上一页](course01)

## Eclipse开发工具（使用JDT开发程序）

在Eclipse里面本身支持有Java项目的开发。

工作目录设置workspace：F:\wcc\javaee

建立MyProject的Java项目

项目创建完成之后，会自动在项目的目录中创建两个子文件夹：

- src： 保存所有的源代码目录；

- bin:  保存所有生成的*.class文件目录；

而在Eclipse之中的src目录就可以进行Java程序的编写；

创建完包和类之后，可以在Windows-》Preferences》Appearance》Colors and Fonts 中调整各个显示框中的字体大小和颜色；

**范例** 编写程序：

- 如果想要生成主方法：main、alt + /；

- 系统输出： sysout、alt + /；

在Eclipse开发项目的时候还可以利用代码生成功能进行通用代码的自动创建，例如：下面创建一个普通的简单Java类。

Source》Generate Getters and Setters ；

Source》Generate Constructor；

Source》Generate toString（）；

快捷键：

- alt + / ：     代码提示；

- alt + 1  ：    代码自动修改建议；

- ctrl + shift + O : 进行开发包的自动导入；

- ctrl + /：　注释当前行代码；

- ctrl + shift + / ： 表示多行注释，去除；

- ctrl + shift + F ： 格式化代码；

- ctrl + shift + L： 快捷键列表；


项目导入或者导出等操作，Java程序最终都要求以*.jar文件的形式给出，这样就要保证在程序类可以进行打包的操作，而这种打包操作可以用Eclipse直接完成。【File】》【Export】

this.project》Properties》Java Build Path 》 Libraries 》 Add External JARs

项目删除，分为两类：

- 从工作区中删除项目，但是该项目仍然存在于磁盘中，可以随后导入；

- 从磁盘中删除项目，项目彻底消失；


初始化参数配置：

Run 》 Run Configurations 》Arguments


## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course03)
