## [上一页](course83)
##  内存操作流（内存流操作）

内存操作流还有一个很小的功能可以实现两个文件的合并处理（文件量不大），因为内存操作流里面最为核心的部分就是将OutputStream输出的数据保存在了程序里面，所以可以通过这一特征进行处理。

现在假设有两个文件： data-a.txt、data-b.txt文件

![](http://ww2.sinaimg.cn/large/0060lm7Tly1fnryyyfxhnj30vd0hk7d4.jpg)

**范例** 实现文件合并处理：

	import java.io.ByteArrayOutputStream;
	import java.io.File;
	import java.io.FileInputStream;
	import java.io.FileOutputStream;
	import java.io.InputStream;
	import java.io.OutputStream;
	
	public class TestDemo {
		public static void main(String[] args) throws Exception {
			File file[]  = new File[] {
					new File("D:" + File.separator + "data-a.txt"),
					new File("D:" + File.separator + "data-b.txt"),
			};
			String data[] = new String[2];//定义一个字符串对象数组
			for (int i = 0; i < data.length; i++) {
				data[i] = readFile(file[i]);//读取数据
			}
			StringBuffer buf = new StringBuffer();
			String contentA[] = data[0].split(" ");//根据空格拆分
			String contentB[] = data[1].split(" ");//根据空格拆分
			OutputStream output = new FileOutputStream(new File("D:" +File.separator + "data.txt"));
			for (int i = 0; i < contentA.length; i++) {
				String str = contentA[i] + "(" + contentB[i] + ") ";
				buf.append(contentA[i]).append("(").append(contentB[i]).append(")").append(" ");
				output.write(str.getBytes());
			}
			output.close();
			System.out.println(buf);
		}
		/**
		 * 如果要读取文件的内容最好传递的是File对象，因为这个对象一定会包含完整名称
		 * @param file
		 * @return
		 */
		public static String readFile(File file) throws Exception{
			if (file.exists()) {
				InputStream input = new FileInputStream(file);
				//这里没有向上转型，因为toByteArray()属于子类扩充的方法
				ByteArrayOutputStream bos = new ByteArrayOutputStream();
				byte data[] = new byte[10];
				int temp = 0;
				while ((temp = input.read(data)) != -1) {//内容都在内存流
					bos.write(data, 0, temp);
				}
				bos.close();
				input.close();
				return new String(bos.toByteArray());
			}
			return null;
		}
	}

**console：**

	Hello(你好) World!(世界！) 

如果只是用InputStream类，在进行数据完整读取的时候会有缺陷，结合内存操作后会好许多，不过这类代码属于上个世纪的代码。

这类的操作随着开发技术的发展出现的越来越少。

## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course85)
