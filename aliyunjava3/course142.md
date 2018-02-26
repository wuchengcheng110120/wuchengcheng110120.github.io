## [上一页](course141)
##  【第21个代码模型】 Map集合（Map接口概述）

Collection集合的特点是每次进行单个对象的保存，现在如果要进行一对对象的保存（couple偶对像）就只能够使用Map对象来完成，所以Map集合中会一次性保存两个，两个对象的关系属于： key = vlaue的结构（键值对）。那么这种结构的最大的特点是可以通过key找到对应的value内容。观察Map接口定义：

public interface Map<K,V>

在Map接口中以下几个常用方法：


- 向集合之中追加数据：public V put(K key, V value)

- 根据key取得对应的value：public V get(Object key)

- 取得所有的key的信息，key不能重复：public Set<K> keySet()

- 取得所有的value，不关注内容是否重复：public Collection<V> values()

- 将Map集合变为Set集合：public Set<Map.Entry<K,V>> entrySet()

Map是一个接口，要使用Map必须通过子类进行对象实例化，而子类有如下的几个：HashMap、HashTable、TreeMap、ConcurrentHashMap四个常用子类


## [返回目录](https://wuchengcheng110120.github.io/aliyunjava3/list)
## [下一页](course143)
