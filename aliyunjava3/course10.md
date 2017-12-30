## [上一页](course09)
## 泛型（通配符）

虽然在类中追加了泛型的定义后避免了ClassCastException的问题，但是又会产生新的情况：
参数的统一问题。

### 范例 观察如下的一段程序：

    package cn.mldn.demo;

    class Message<T>{
      private T note;

      public T getNote() {
        return note;
      }

      public void setNote(T note) {
        this.note = note;
      }
    }
    public class TestDemo {
      /**
       * @param args
       */
      public static void main(String[] args) {
        Message<String> msg = new Message<String>();
        msg.setNote("天天很帅气！");
        fun(msg);
      }
      public static void fun(Message<String> temp){
        System.out.println(temp.getNote());
      }
    }

但是这样会带来一个新的问题，如果现在泛型的类型设置的不是String，而是Integer（泛型只允许设置类和接口，而不允许使用基本数据类型）。

### 范例 错误的代码：

    public class TestDemo {
      /**
       * @param args
       */
      public static void main(String[] args) {
        Message<Integer> msg = new Message<Integer>();
        msg.setNote(99); 
        fun(msg);//出现错误，因为只能够接受String
      }
      public static void fun(Message<String> temp){
        System.out.println(temp.getNote());
      }
    }

![](https://s1.ax1x.com/2017/12/31/pSemsU.png)

既然泛型造成了类型的困扰那就不再设置泛型？

package cn.mldn.demo;

class Message<T>{
	private T note;

	public T getNote() {
		return note;
	}

	public void setNote(T note) {
		this.note = note;
	}
}
public class TestDemo {
	/**
	 * @param args
	 */
	public static void main(String[] args) {
		Message<Integer> msg = new Message<Integer>();
		msg.setNote(99); 
		fun(msg);//出现错误，因为只能够接受String
	}
	//如果没有设置泛型类型，那么默认用的类型就是Object 
	public static void fun(Message temp){
		temp.setNote("天天很帅气！");
		System.out.println(temp.getNote());
	}
}
## console：

    天天很帅气！
    
所以得出我们需要的解决方案：可以接收所有的泛型类型，又不能让用户任意修改。
那么就需要通配符来实现，使用“？”来处理

    public class TestDemo {
      /**
       * @param args
       */
      public static void main(String[] args) {
        Message<Integer> msg = new Message<Integer>();
        msg.setNote(99); 
        fun(msg);
      }
      //此时使用通配符“？”，描述的是它可以接受任意类型，由于不确定类型，所以无法修改
      public static void fun(Message<?> temp){
        System.out.println(temp.getNote());
      }
    }
而在“？”的基础上又产生了两个子通配符：

- ？extends类 设置泛型上限：
        |-例如： ？extends Number，表示只能够设置Number或其子类，例如Integer、Double等；
        
- ？super类 设置泛型下限：
        |-例如： ？super String，表示只能够设置String或其父类：Object。
        

### 范例 观察泛型上限：

        package cn.mldn.demo;

        class Message<T extends Number>{//设置泛型上限
          private T note;

          public T getNote() {
            return note;
          }

          public void setNote(T note) {
            this.note = note;
          }
        }
        public class TestDemo {
          /**
           * @param args
           */
          public static void main(String[] args) {
            Message<Integer> msg = new Message<Integer>();
            msg.setNote(99); 
            fun(msg);
          }
          //此时使用通配符“？”，描述的是它可以接受任意类型，由于不确定类型，所以无法修改
          public static void fun(Message<? extends Number> temp){
            System.out.println(temp.getNote());
          }
        }
        
### 范例 设置泛型下限：

        package cn.mldn.demo;

        class Message<T>{//设置泛型下限
          private T note;

          public T getNote() {
            return note;
          }

          public void setNote(T note) {
            this.note = note;
          }
        }
        public class TestDemo {
          /**
           * @param args
           */
          public static void main(String[] args) {
            Message<String> msg = new Message<String>();
            msg.setNote("Hello World !"); 
            fun(msg);
          }
          //此时使用通配符“？”，描述的是它可以接受任意类型，由于不确定类型，所以无法修改
          public static void fun(Message<? super String> temp){
            System.out.println(temp.getNote());
          }
        }
要求理解，并不要求立刻在代码中使用



## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course11)
