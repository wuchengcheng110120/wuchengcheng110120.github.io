## [上一页](course11)
## 泛型（泛型方法）

在定义的类和接口中发现都可以在里面的方法中使用泛型，这种方法就称为泛型方法，但是泛型方法不一定非定义在
泛型类或者泛型接口中，也可以单独定义。

### 范例  定义泛型方法：

        package cn.mldn.demo;

        public class TestDemo {
          public static void main(String[] args) {
            Integer data[] = fun(1,2,3,4);
            for(int temp : data){
              System.out.println(temp);
            }
          }
          //<T>描述的是泛型标记的声明
          public static <T>T[]  fun(T... args){
            return args;
          }
        }
建议不要使用此类方法，了解即可；




## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course13)

