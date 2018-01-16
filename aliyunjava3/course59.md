## [上一页](course58)
## 观察者设计模式

观察者设计模式可以理解为一触即发

如果想要实现观察者设计模式，需要一下两个程序结构：

- 观察者：java.util.Observer

- 被观察者：java.util.Observable

**范例** 实现观察者：

    package cn.mldn.demo;

    import java.util.Observable;
    import java.util.Observer;

    class Person implements Observer{//这些是所有的观察者
      public void update(Observable o, Object arg) {//一旦关注的事情发生变化
        if (o instanceof House) {//如果发现被观察者House发生改变
          if (arg instanceof Double) {
            System.out.println("【人们关注房子】房价上涨  新价格 ：" + arg );
          }
        }
      }
    }

    class House extends Observable{
      private double price;
      public House(double price){
        this.price =price;
      }
      public void setPrice(double price){
        if (price > this.price) {//价格上涨
          super.setChanged();//现在关注的内容改变了
          super.notifyObservers(price);//唤醒所有的观察者
        }
        this.price = price;
      }
    }

    public class TestDemo {
      public static void main(String [] args) throws Exception {
        Person perA = new Person();
        Person perB = new Person();
        Person perC = new Person();
        House house = new House(80000.00);
        house.addObserver(perA);// 必须手工设置观察者
        house.addObserver(perB);
        house.addObserver(perC);
        house.setPrice(150000.00);
      }
    }
**console:**

    【人们关注房子】房价上涨  新价格 ：150000.0
    【人们关注房子】房价上涨  新价格 ：150000.0
    【人们关注房子】房价上涨  新价格 ：150000.0

这种设计模式在现在的开发中意义已经不是很大了，希望大家能理解观察者设计模式即可。




## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course60)
