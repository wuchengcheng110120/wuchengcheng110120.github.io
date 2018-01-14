## [上一页](course55)
## 国际化程序（locale类）

java.util.local主要是进行本地区域定位的，也就是说想要读取指定的区域资源文件，就必须依靠local完成；

首先来观察locale类的定义：

public final class Locale
extends Object
implements Cloneable, Serializable

The Locale class provides three constructors:

     Locale(String language)
     Locale(String language, String country)
     Locale(String language, String country, String variant)
     
- local类构造: Locale(String language, String country),设置语言和国家；

**范例** 观察中文中国：

    package cn.mldn.demo;

    import java.util.Locale;

    public class TestDemo {
       public static void main(String[] args) {
          System.out.println(Locale.US);//en_US
          System.out.println(Locale.ENGLISH);//en
          System.out.println(Locale.CHINA);//zh_CN
          System.out.println(Locale.CHINESE);//zh
      }
    }
IE工具栏中Internet选项中语言首选项-添加语言中有关于所有国家和语言的描述：

- 取得当前的locale对象：public static Locale getDefault()；

通过locale类来设置当前的语言和国家，从而选择正确的资源文件。


## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course57)
