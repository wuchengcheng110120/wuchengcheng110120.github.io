## [上一页](course10)
## 泛型（泛型接口）

泛型除了定义在类中还可以定义在接口里面，那么这种情况称为泛型接口。

### 范例 定义一个泛型接口：

    interface IMessage <T>{//在接口上定义了泛型
      public void print(T t);
    }
    
 但是对于这个接口的实现子类有两种做法：
 
 ### 范例  1在子类定义的时候继续使用泛型：
 
     package cn.mldn.demo;

    interface IMessage <T>{//在接口上定义了泛型
      public void print(T t);
    }
    class MessageImpl<T> implements IMessage<T>{
      @Override
      public void print(T t) {
        System.out.println(t);
      }
    }
    public class TestDemo {
      /**
       * @param args
       */
      public static void main(String[] args) {
        IMessage<String> msg = new MessageImpl<String>();
        msg.print("Hello World !");
      }
    }
    
### 范例  2在子类实现接口的时候明确使用类型：

    package cn.mldn.demo;

    interface IMessage <T>{//在接口上定义了泛型
      public void print(T t);
    }
    class MessageImpl implements IMessage<String>{
      @Override
      public void print(String t) {
        System.out.println(t);
      }
    }
    public class TestDemo {
      /**
       * @param args
       */
      public static void main(String[] args) {
        IMessage<String> msg = new MessageImpl();
        msg.print("Hello World !");
      }
    }
    
以后编写的程序一定会使用泛型接口。





## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course12)
