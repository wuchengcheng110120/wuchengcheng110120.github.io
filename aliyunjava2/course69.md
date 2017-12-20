## [上一页](course68)

## 接口的定义与使用（使用接口定义标准）

对于接口在实际的开发之中有三大核心应用环境：

- 定义操作标准；

- 表示能力；

-在分布式开发之中暴露远程服务方法。

现在要求描述出一个概念:电脑上可以使用任何usb设备（U盘、打印机、风扇...）

![](https://i.imgur.com/txhvO46.png)

**范例** 定义一个USB标准：

	interface USB{
		public void setup();//安装USB的驱动
		public void work();//进行工作
	}

**范例** 定义电脑类：

	class Computer{
		public void plugin(USB usb) {//只能够插USB设备
			usb.setup();//安装
			usb.work();//工作
		}
	}

电脑类在诞生的时候是不关注USB设备有哪些的。

**范例** 定义USB子类：

	class Flash implements USB{//定义一个USB设备
		public void setup() {
			System.out.println("安装U盘驱动！");
		}
		public void work() {
			System.out.println("进行数据传输！ ");
		}
	}
	class Print implements USB{//定义一个USB设备
		public void setup() {
			System.out.println("安装U盘驱动！");
		}
		public void work() {
			System.out.println("进行文件打印！ ");
		}
	}

**范例** 测试类：

	public class TestDemo {
		public static void main(String[] args) {
			Computer com = new Computer();
			com.plugin(new Flash());
			com.plugin(new Print());
		}
	}

**console：**

	安装U盘驱动！
	进行数据传输！ 
	安装U盘驱动！
	进行文件打印！

发现使用接口和对象多态性的概念结合之后，对于参数的统一更加明确了。而且可以发现接口是设计在类之上的设计抽象。
![](https://i.imgur.com/lIPZ6LD.png)

接口是一个标准，正常的开发先设计接口，再写类。

## [返回目录](https://wuchengcheng110120.github.io/learnJava)
## [下一页](course70)
