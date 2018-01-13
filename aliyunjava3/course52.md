## [上一页](course51)
## 比较器（Comparable）

对于比较器给出一个明确的定义：只存在于原理分析上，在实际开发中使用意义不大；

如果想要进行数组操作Arrays类可以提供很好的支持，但是Arrays类中有这样一个方法：

- 对象数组排序：public static void sort(Object[] a)

ClassCastException - if the array contains elements that are not mutually comparable (for example, strings and integers)

     package cn.mldn.demo;

      import java.util.Arrays;

      class Person{
        private String name;
        private int age;
        public Person(String name, int age) {
          super();
          this.name = name;
          this.age = age;
        }
        @Override
        public String toString() {
          return "Person [name=" + name + ", age=" + age + "]";
        }

      }
      public class TestDemo {
        public static void main(String[] args) {
          Person per[] = new Person[]{
              new Person("张三",20),
              new Person("李四",19),
              new Person("王五",21)
              };//对象数组
          Arrays.sort(per);//要进行对象数组的排序处理
          System.out.println(Arrays.toString(per));
        }
      }

**console：**

      Exception in thread "main" java.lang.ClassCastException: cn.mldn.demo.Person cannot be cast to java.lang.Comparable
            at java.util.ComparableTimSort.countRunAndMakeAscending(ComparableTimSort.java:320)
            at java.util.ComparableTimSort.sort(ComparableTimSort.java:188)
            at java.util.Arrays.sort(Arrays.java:1246)
            at cn.mldn.demo.TestDemo.main(TestDemo.java:26)
       
 这个时候对象所在的类必须实现Comparable接口，而Comparable接口定义如下：
 
      public interface Comparable<T>
      
      public interface Comparable<T>{
            int compareTo(T o);
      }

实现Comparable接口的类中有常用的：Date、String、Integer等类

String中的compareTo就是覆写Comparable接口的方法

![](http://ww2.sinaimg.cn/large/0060lm7Tly1fnfakgjoouj30mw0dg40n.jpg)

**范例** 实现对象数组排序：

      package cn.mldn.demo;

      import java.util.Arrays;

      class Person implements Comparable<Person>{
            private String name;
            private int age;
            public Person(String name, int age) {
                  super();
                  this.name = name;
                  this.age = age;
            }
            @Override
            public String toString() {
                  return "Person [name=" + name + ", age=" + age + "]\n";
            }
            public int compareTo(Person o) {
                  if (this.age > o.age) {
                        return 1;
                  }else if (this.age < o.age) {
                        return -1;
                  } else{
                        return 0;
                  }
            }

      }
      public class TestDemo {
            public static void main(String[] args) {
                  Person per[] = new Person[]{
                              new Person("张三",20),
                              new Person("李四",19),
                              new Person("王五",21)
                              };//对象数组
                  Arrays.sort(per);//要进行对象数组的排序处理
                  System.out.println(Arrays.toString(per));
            }
      }
 **console:**
 
      [Person [name=李四, age=19]
      , Person [name=张三, age=20]
      , Person [name=王五, age=21]
      ]

结论：只要是对象数组排序就必须有Comparable接口







## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course53)
