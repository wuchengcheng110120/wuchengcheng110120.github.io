## [上一页](course53)
## 比较器（Comparator）

Comparable这种比较器的核心价值在于，当一个类定义时就已经明确好了这个类的数据保存是需要排序的，但是很多情况下一个类设计的时候有可能没有考虑到
排序的需求；

**范例** 定义一个类：

    class Person {
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
      public String getName() {
        return name;
      }
      public void setName(String name) {
        this.name = name;
      }
      public int getAge() {
        return age;
      }
      public void setAge(int age) {
        this.age = age;
      }
    }
    
 这个时候不能使用Arrays.sort()进行排序，如果必须使用Arrays.sort()进行排序，而且不能修改Person类，所以这个时候的排序就属于挽救排序的功能。
 
 使用java.util.Comparator,这个接口定义如下：
 
    @FunctionalInterface
    public interface Comparator<T>{
      public int compare(T o1, T o2);
      public boolean equals(Object obj);
    }
    
要想使用这个接口就必须定义一个排序的子类完成；

**范例** 定义一个为Person实现排序的功能类：

    class PersonComparator implements Comparator<Person>{
      public int compare(Person o1, Person o2) {
        if (o1.getAge() > o2.getAge()) {
          return 1;
        }else if (o1.getAge() < o2.getAge()) {
          return -1;
        }
        return 0;
      }
    }

排序的操作还是在Arrays里面，只不过更换一个新的方法：

- 排序：public static <T> void sort(T[] a,
                            Comparator<? super T> c)

**范例** 排序：

  public class TestDemo {
    public static void main(String[] args) {
      Person per[] = new Person[]{
          new Person("张三",20),
          new Person("李四",19),
          new Person("王五",21)
          };//对象数组
      Arrays.sort(per, new PersonComparator());//要进行对象数组的排序处理
      System.out.println(Arrays.toString(per));
    }
  }

**console：**

    [Person [name=李四, age=19]
    , Person [name=张三, age=20]
    , Person [name=王五, age=21]
    ]

请解释两种比较器的区别？

- java.lang.Comparable：是在一个类定义的时候默认实现好的方法，里面有compareTo()方法;

- java.util.Comparator：挽救的比较接口，需要定义一个比较规则类，定义有compare()方法、equals()方法；

以后在进行分析时使用的最多的还是Comparable


## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course55)
