面试问题：拿下

# 主题1： Java基础

### 前言

这一主题主要记录关于Java基础的各个方面的面试题。

> 比如：在 Java 中除了以 Map 结尾的类之外， 其他类都实现了 Collection 接口。并且，以 Map 结尾的类都实现了 Map 接口。
>
> 问题的解答（Q&A会用以下的方式给出），当然下面这道题也可能出现在面试问题中。

#### 1. String::intern()

* String::intern() 是一个native本地方法
* 它的作用是：如果字符串常量池中已经包含一个等于此String对象的字符串，则返回代表池中这个对象的Sting对象的引用；
* 否则，会将此String对象包含的字符串添加到常量池中，并且返回此String对象引用。

```java
public static void main(String[] args) {
    String str1 = new StringBuilder("58").append("tongcheng").toString();
    System.out.println(str1);
    System.out.println(str1.intern());
    System.out.println(str1 == str1.intern());


    String str2 = new StringBuilder("ja").append("va").toString();
    System.out.println(str2);
    System.out.println(str2.intern());
    System.out.println(str2 == str2.intern());
}
```

### 正式开始 》》》

#### 1. List、Set和Map的区别

* List可以有重复的对象，Set不可以有重复的对象
* List元素是有序的，Set没法保证有序
* List可以插入多个null值，Set只能插入一个
* Map,key-value的键值对，entry对象形式，key是无序，不可重复的；value是无序，可重复的；

##### 1.1 List实现有三种：对应的数据结构

* ArrayList： Object[]数组
* Vector： Object[]数组
* LinkedList： 双向链表

##### 1.2 Set实现：对应的数据结构

* HashSet（无序，唯一）: 基于 HashMap 实现的，底层采用 HashMap 来保存元素
* LinkedHashSet：LinkedHashSet 是 HashSet 的子类，并且其内部是通过 LinkedHashMap 来实现的。
* TreeSet（有序，唯一）： 红黑树(自平衡的排序二叉树)

##### 1.3 Map实现：对应的数据结构

* HashMap： JDK1.8 之前 HashMap 由数组+链表组成的，数组是 HashMap 的主体，链表则是主要为了解决哈希冲突而存在的（“拉链法”解决冲突）。JDK1.8 以后在解决哈希冲突时有了较大的变化，当链表长度大于阈值（默认为 8）（将链表转换成红黑树前会判断，如果当前数组的长度小于 64，那么会选择先进行数组扩容，而不是转换为红黑树）时，将链表转化为红黑树，以减少搜索时间。
* LinkedHashMap： LinkedHashMap 继承自 HashMap，所以它的底层仍然是基于拉链式散列结构即由数组和链表或红黑树组成。另外，LinkedHashMap 在上面结构的基础上，增加了一条双向链表，使得上面的结构可以保持键值对的插入顺序。同时通过对链表进行相应的操作，实现了访问顺序相关逻辑。
* Hashtable： 数组+链表组成的，数组是 HashMap 的主体，链表则是主要为了解决哈希冲突而存在的；与HashMap的区别是Hashtable线程安全，但效率低。
* TreeMap： 红黑树（自平衡的排序二叉树）

##### 1.4 使用时如何选择集合

​		当我们需要保存一组类型相同的数据的时候，我们应该是用一个容器来保存，这个容器就是数组，但是，使用数组存储对象具有一定的弊端， 因为我们在实际开发中，存储的数据的类型是多种多样的，于是，就出现了“集合”，集合同样也是用来存储多个数据的。数组的缺点是一旦声明之后，长度就不可变了；同时，声明数组时的数据类型也决定了该数组存储的数据的类型；而且，数组存储的数据是有序的、可重复的，特点单一。 但是集合提高了数据存储的灵活性，Java 集合不仅可以用来存储不同类型不同数量的对象，还可以保存具有映射关系的数据。

* 根据集合的特点来选用，比如我们需要根据键值获取到元素值时就选用 Map 接口下的集合，需要排序时选择 TreeMap,不需要排序时就选择 HashMap,需要保证线程安全就选用 ConcurrentHashMap。
* 只需要存放元素值时，就选择实现Collection 接口的集合，需要保证元素唯一时选择实现 Set 接口的集合比如 TreeSet 或 HashSet，不需要就选择实现 List 接口的比如 ArrayList 或 LinkedList，然后再根据实现这些接口的集合的特点来选用

#### 2. 迭代器Iterrator

* Iterator 主要是用来遍历集合用的
* 特点是更加安全，因为它可以确保，在当前遍历的集合元素被更改的时候，就会抛出 ConcurrentModificationException 异常。

#### 3. 集合的线程安全

Arraylist ,LinkedList,Hashmap,HashSet,TreeSet,TreeMap，PriorityQueue 都不是线程安全的，Vector，HashTable是线程安全的，但是性能低。要使用线程安全的集合的话， java.util.concurrent 包中提供了很多并发容器：

* ConcurrentHashMap：可以看作是线程安全的 HashMap;
* CopyOnWriteArrayList：可以看作是线程安全的 ArrayList，在读多写少的场合性能非常好，远远好于 Vector;
* ConcurrentLinkedQueue：高效的并发队列，使用链表实现。可以看做一个线程安全的 LinkedList，这是一个非阻塞队列；
* BlockingQueue：这是一个接口，JDK 内部通过链表、数组等方式实现了这个接口。表示阻塞队列，非常适合用于作为数据共享的通道；
* ConcurrentSkipListMap：跳表的实现。这是一个Map，使用跳表的数据结构进行快速查找。

#### 4. ArrayList 和 Vector 和 LinkedList 的区别

* **是否保证线程安全：** ArrayList 和 LinkedList 都是不同步的，也就是不保证线程安全；Vector是线程安全的。
* **底层数据结构：** Arraylist 和Vector 底层使用的是 **Object** **数组**；LinkedList 底层使用的是 **双向链表**（JDK1.6 之前为循环链表，JDK1.7 取消了循环。注意双向链表和双向循环链表的区别，下面有介绍到！）
* **插入和删除是否受元素位置的影响：** **①** **ArrayList** 采用数组存储，所以插入和删除元素的时间复杂度受元素位置的影响。 比如：执行add(E e)方法的时候， ArrayList 会默认在将指定的元素追加到此列表的末尾，这种情况时间复杂度就是 O(1)。但是如果要在指定位置 i 插入和删除元素的话（add(int index, E element)）时间复杂度就为 O(n-i)。因为在进行上述操作的时候集合中第 i 和第 i 个元素之后的(n-i)个元素都要执行向后位/向前移一位的操作。 ② **LinkedList** 采用链表存储，所以对于add(E e)方法的插入，删除元素时间复杂度不受元素位置的影响，近似 O(1)，如果是要在指定位置i插入和删除元素的话（(add(int index, E element)） 时间复杂度近似为o(n))因为需要先移动到指定位置再插入。
* **是否支持快速随机访问：** LinkedList 不支持高效的随机元素访问，而 ArrayList 支持。快速随机访问就是通过元素的序号快速获取元素对象(对应于get(int index)方法)。
* **内存空间占用：** ArrayList 的空 间浪费主要体现在在 list 列表的结尾会预留一定的容量空间，而 LinkedList 的空间花费则体现在它的每一个元素都需要消耗比 ArrayList 更多的空间（因为要存放直接后继和直接前驱以及数据）。

#### 5. comparable 和 comparator的区别

* comparable 接口实际上是出自java.lang包 它有一个 compareTo(Object obj)方法用来排序
* comparator接口实际上是出自 java.util 包它有一个compare(Object obj1, Object obj2)方法用来排序
* 一般我们需要对一个集合使用自定义排序时，我们就要重写compareTo()方法或compare()方法，当我们需要对某一个集合实现两种排序方式，比如一个 song 对象中的歌名和歌手名分别采用一种排序方法的话，我们可以重写compareTo()方法和使用自制的Comparator方法或者以两个 Comparator 来实现歌名排序和歌星名排序，第二种代表我们只能使用两个参数版的 Collections.sort().

#### 6. HashSet 、LinkedHashSet 和 TreeSet 的区别

* HashSet 是 Set 接口的主要实现类 ，HashSet 的底层是 HashMap，线程不安全的，可以存储 null 值；
* LinkedHashSet 是 HashSet 的子类，能够按照添加的顺序遍历；
* TreeSet 底层使用红黑树，能够按照添加元素的顺序进行遍历，排序的方式有自然排序和定制排序。

#### 7. HashMap 和 HashTable 的区别

* **线程是否安全：** HashMap 是非线程安全的，HashTable 是线程安全的。因为 HashTable 内部的方法基本都经过synchronized 修饰。（如果你要保证线程安全的话就使用 ConcurrentHashMap 吧！）；
* **效率：** 因为线程安全的问题，HashMap 要比 HashTable 效率高。另外，HashTable 基本被淘汰，不要在代码中使用它；**对 Null key 和 Null value 的支持：** HashMap 可以存储 null 的 key 和 value，但 null 作为键只能有一个，null 作为值可以有多个；HashTable 不允许有 null 键和 null 值，否则会抛出 NullPointerException。
* **初始容量大小和每次扩充容量大小的不同 ：** ① 创建时如果不指定容量初始值，Hashtable 默认的初始大小为 11，之后每次扩充，容量变为原来的 2n+1。HashMap 默认的初始化大小为 16。之后每次扩充，容量变为原来的 2 倍。② 创建时如果给定了容量初始值，那么 Hashtable 会直接使用你给定的大小，而 HashMap 会将其扩充为 2 的幂次方大小（HashMap 中的tableSizeFor()方法保证，下面给出了源代码）。也就是说 HashMap 总是使用 2 的幂作为哈希表的大小,后面会介绍到为什么是 2 的幂次方。
* **底层数据结构：** JDK1.8 以后的 HashMap 在解决哈希冲突时有了较大的变化，当链表长度大于阈值（默认为 8）（将链表转换成红黑树前会判断，如果当前数组的长度小于 64，那么会选择先进行数组扩容，而不是转换为红黑树）时，将链表转化为红黑树，以减少搜索时间。Hashtable 没有这样的机制。

#### 8. ConcurrentHashMap 和 HashTable 的区别

* **底层数据结构：** JDK1.7 的 ConcurrentHashMap 底层采用 **分段的数组+链表** 实现，JDK1.8 采用的数据结构跟 HashMap1.8 的结构一样，数组+链表/红黑二叉树。Hashtable 和 JDK1.8 之前的 HashMap 的底层数据结构类似都是采用 **数组+链表** 的形式，数组是 HashMap 的主体，链表则是主要为了解决哈希冲突而存在的；

* **实现线程安全的方式（重要）：** ① **在 JDK1.7 的时候，ConcurrentHashMap（分段锁）** 对整个桶数组进行了分割分段(Segment)，每一把锁只锁容器其中一部分数据，多线程访问容器里不同数据段的数据，就不会存在锁竞争，提高并发访问率。 **到了 JDK1.8 的时候已经摒弃了 Segment 的概念，而是直接用 Node 数组+链表+红黑树的数据结构来实现，并发控制使用 synchronized 和 CAS 来操作。（JDK1.6 以后 对 synchronized 锁做了很多优化）** 整个看起来就像是优化过且线程安全的 HashMap，虽然在 JDK1.8 中还能看到 Segment 的数据结构，但是已经简化了属性，只是为了兼容旧版本；② **Hashtable(同一把锁)** :使用 synchronized 来保证线程安全，效率非常低下。当一个线程访问同步方法时，其他线程也访问同步方法，可能会进入阻塞或轮询状态，如使用 put 添加元素，另一个线程不能使用 put 添加元素，也不能使用 get，竞争会越来越激烈效率越低。
* ConcurrentHashMap 取消了 Segment 分段锁，采用 CAS 和 synchronized 来保证并发安全。数据结构跟 HashMap1.8 的结构类似，数组+链表/红黑二叉树。Java 8 在链表长度超过一定阈值（8）时将链表（寻址时间复杂度为 O(N)）转换为红黑树（寻址时间复杂度为 O(log(N))）; synchronized 只锁定当前链表或红黑二叉树的首节点，这样只要 hash 不冲突，就不会产生并发，效率又提升 N 倍。

#### 9. Collections 工具类

* 作用：排序

```java
//反转
void reverse(List list)
//随机排序
void shuffle(List list)
//按自然排序的升序排序
void sort(List list)
//定制排序，由Comparator控制排序逻辑
void sort(List list, Comparator c)
//交换两个索引位置的元素
void swap(List list, int i , int j)
//旋转。当distance为正数时，将list后distance个元素整体移到前面。当distance为负数时，将 list的前distance个元素整体移到后面
void rotate(List list, int distance)
```

* 作用：查找,替换操作

```java
//对List进行二分查找，返回索引，注意List必须是有序的
int binarySearch(List list, Object key)
//根据元素的自然顺序，返回最大的元素。
int max(Collection coll)
//类比，返回最小的元素
int min(Collection coll)
//根据定制排序，返回最大元素，排序规则由Comparatator类控制。
int max(Collection coll, Comparator c)
//类比
int min(Collection coll, Comparator c)
//用指定的元素代替指定list中的所有元素。
void fill(List list, Object obj)
//统计元素出现次数
int frequency(Collection c, Object o)
//统计target在list中第一次出现的索引，找不到则返回-1
int indexOfSubList(List list, List target)
//类比
int lastIndexOfSubList(List source, list target)
//用新元素替换旧元素
boolean replaceAll(List list, Object oldVal, Object newVal)
```

* 作用：同步控制(不推荐，需要线程安全的集合类型时请考虑使用 JUC 包下的并发集合)

```java
//返回指定 collection 支持的同步（线程安全的）collection。
synchronizedCollection(Collection<T>  c) 
//返回指定列表支持的同步（线程安全的）List。
synchronizedList(List<T> list)
//返回由指定映射支持的同步（线程安全的）Map。
synchronizedMap(Map<K,V> m) 
//返回指定 set 支持的同步（线程安全的）set。
synchronizedSet(Set<T> s) 
```

#### 10. HashSet是如何保证不重复的

判断两个对象是不是重复的，主要依靠的是hashCode方法和equals方法，所以，一个对象如果想通过HashSet方法判断是不是重复的，需要重写hashCode方法和equals方法。

* 如果hashCode不同，说明是新元素，存
* 如果hashCode相同，且equals也相同，就说明元素存在，就不存
* 如果hashCode相同，但equals不同，说明元素不存在，存

#### 11. HashMap是线程安全的吗，为什么不是线程安全的（最好画图说明多线程环境下不安全）?

* HashMap是一个用于存储Key-Value键值对的集合， 每一个键值对也叫做**Entry**
* 使用Hashmap进行put操作可能会引起死循环，导致CPU利用率接近100%
* **HashMap 是非线程安全的**，同时我们知道 HashTable 是线程安全的，因为里面的方法使用了 **synchronized 进行同步**。
* HashMap 底层是一个 Entry 数组，当发生 hash 冲突的时候，HashMap 是采用链表的方式来解决的，在对应的数组位置存放链表的头结点。对链表而言，新加入的节点会从头结点加入。

#### 12. HashMap的扩容过程；为什么是2的幂次方

* 为了能让 HashMap 存取高效，尽量较少碰撞，也就是要尽量把数据分配均匀。
* 通过resize()方法进行扩容，容量规则为2的幂次
* 因为2的幂次方容量，对于哈希值的散列更均匀，int hash = key.hashCode(); int index = hash & (n-1);

#### 13. HashMap1.7与1.8的区别，说明1.8做了哪些优化，如何优化的？

* **JDK1.7用的是头插法，而JDK1.8及之后使用的都是尾插法，** **在JDK1.8之后是因为加入了红黑树使用尾插法，能够避免出现逆序且链表死循环的问题**
*  JDK1.8 之后在解决哈希冲突时有了较大的变化，当链表长度大于阈值（默认为 8）（将链表转换成红黑树前会判断，如果当前数组的长度小于 64，那么会选择先进行数组扩容，而不是转换为红黑树）时，将链表转化为红黑树，以减少搜索时间。
* **扩容后数据存储位置的计算方式也不一样**
* JDK1.8 之前 HashMap 底层是 **数组和链表** 结合在一起使用也就是 **链表散列**。**HashMap 通过 key 的 hashCode 经过hash运算处理过后得到 hash 值，然后通过 (n - 1) & hash 判断当前元素存放的位置（这里的 n 指的是数组的长度），如果当前位置存在元素的话，就判断该元素与要存入的元素的 hash 值以及 key 是否相同，如果相同的话，直接覆盖，不相同就通过拉链法解决冲突。**
* TreeMap、TreeSet 以及 JDK1.8 之后的 HashMap 底层都用到了红黑树。红黑树就是为了解决二叉查找树的缺陷，因为二叉查找树在某些情况下会退化成一个线性结构。

#### 14. final finally finalize

* final用于声明属性，方法和类，分别表示属性不可变，方法不可覆盖，类不可继承。
* finally是异常处理语句结构的一部分，try...catch...finally表示总是执行。
* finalize是Object类的一个方法，在垃圾收集器执行的时候会调用被回收对象的此方法，供垃圾收集时的其他资源回收，例如关闭文件等。

#### 15.强引用、软引用、弱引用、虚引用   

Java中提供这四种引用类型主要有两个目的：第一是可以让程序员通过代码的方式决定某些对象的生命周期；第二是有利于JVM进行垃圾回收。

* **强引用：** 如果一个对象具有强引用，那就类似于**必不可少的**物品，不会被垃圾回收器回收。
* **软引用：** 软引用是用来描述一些**有用但并不是必需**的对象，在Java中用java.lang.ref.SoftReference类来表示。对于软引用关联着的对象，只有在内存不足的时候JVM才会回收该对象。因此，这一点可以很好地用来解决OOM的问题，并且这个特性很适合用来实现缓存：比如网页缓存、图片缓存等。
* **弱引用：** 弱引用也是用来描述**非必需对象**的，当JVM进行垃圾回收时，无论内存是否充足，都会回收被弱引用关联的对象。

**虚引用：** 如果一个对象与虚引用关联，则跟没有引用与之关联一样，在任何时候都可能被垃圾回收器回收。虚引用主要用来跟踪对象被垃圾回收的活动。

#### 16. Java反射

* Java反射机制是在运行状态中，对于任意一个类，都能够知道这个类的所有属性和方法；对于任意一个对象，都能够调用它的任意一个方法和属性；这种**动态获取的信息以及动态调用对象的方法的功能**称为Java语言的反射机制。

#### 17.  Arrays.sort实现原理 和 Collection.sort实现原理

* 不论是Collections.sort方法或者是Arrays.sort方法，底层实现都是**TimSort**实现的，这是jdk1.7新增的，以前是归并排序。TimSort算法就是找到已经排好序数据的子序列，然后对剩余部分排序，然后合并起来.

#### 18.LinkedHashMap 的应用

* HashMap是无序的，当我们希望有顺序地去存储key-value时，就需要使用LinkedHashMap
* LinkedHashMap继承了HashMap
* LinkedHashMap就是HashMap+双向链表
* LinkedHashMap也是线程不安全的（需要 synchronized 进行了同步）

#### 19.cloneable接口实现原理

* Cloneable是一个标记接口，里面没有任何的方法。
* 如果要使用Cloneable实现拷贝功能，需要先实现这个接口，然后重写Object的clone方法
* 对于类中的引用类型的属性，需要在clone方法中实现深拷贝，否则就是浅拷贝

#### 20. 异常分类以及处理机制

Exception和Error都继承一个父类Throwable，异常又分为运行时异常和非运行时异常。

* **异常**是指程序运行过程中发生的一些不正常事件（如除0溢出，数组下标越界，所要读取的文件不存在）。
* **抛出异常：**Java程序的执行过程中如果出现异常事件，可以生成一个异常类对象，该对象封装了异常事件的信息，并将其提交给Java运行系统，这个过程称为抛出异常，不处理的话会直接导致程序中断。
* **Error：** Error是无法处理的异常，比如OutOfMemoryError，一般发生这种异常，JVM会选择终止程序。因此我们编写程序时不需要关心这类异常。
* **Exception：** 就是我们经常见到的一些异常情况，这些异常是我们可以处理的异常，是所有异常类的父类。
* **unchecked exception（非受查异常）**：包括Error和RuntimeException，比如常见的NullPointerException、IndexOutOfBoundsException。对于RuntimeException，java编译器不要求必须进行异常捕获处理或者抛出声明，由程序员自行决定。
* **checked exception（受查异常）**：也称非运行时异常（运行时异常以外的异常就是非运行时异常），由代码能力之外的因素导致的运行时错误。java编译器强制程序员必须进行捕获处理，比如常见的有IOExeption和SQLException。如果不进行捕获或者抛出声明处理，编译都不会通过。
* 典型的**RuntimeException**：包括NullPointerException、IndexOutOfBoundsException、IllegalArgumentException等。
* 典型的**非RuntimeException：**包括IOException、SQLException等。
* **异常处理机制**：
  * 1.**捕获机制：try-catch-finally**
  * 2.**抛出：throw，throws**：throw：手动抛出异常，一般由程序员在方法内抛出Exception的子类异常。throws：声明在方法名之后，告诉调用者，该方法可能会抛出异常，也就是说异常发生后会抛给调用者，由调用者处理异常。

#### 21. wait和sleep的区别

* sleep来自Thread类，wait来自Object类。
* sleep方法没有**释放锁**，而wait方法释放了锁，使得其他线程可以使用同步控制块或者方法。
* **使用范围：**wait，notify和notifyAll只能在同步控制方法或者同步控制块里面使用，而sleep可以在任何地方使用。
* sleep必须**捕获异常**，而wait，notify和notifyAll不需要捕获异常

#### 22. 数组在内存中如何分配

* 数组也是对象，所以放在堆中，new创建会在堆中分配内存空间，并返回一个引用

* 同时栈中会存储数组的地址指针（引用）

#### 23.解决hash冲突的方法：

* 1.开放定址法（线性探测再散列，二次探测再散列，伪随机探测再散列）
* 2.再哈希法
* 3.链地址法(Java hashmap就是这么做的)
* 4.建立一个公共溢出区

#### 24. String、StringBuilder、StringBuffer的区别

* 操作少量的数据: 适用 String
* 单线程操作字符串缓冲区下操作大量数据: 适用 StringBuilder
* 多线程操作字符串缓冲区下操作大量数据: 适用 StringBuffer
* String 中的对象是不可变的，也就可以理解为常量，线程安全。
* StringBuffer 对方法加了同步锁或者对调用的方法加了同步锁，所以是线程安全的。
* StringBuilder 并没有对方法进行加同步锁，所以是非线程安全的。
* String 类中使用 final 关键字修饰字符数组来保存字符串，String对象不可变； 
* StringBuilder 与 StringBuffer的对象是可变的。

#### 25. Object类

```java
//native方法，用于返回当前运行时对象的Class对象，使用了final关键字修饰，故不允许子类重写。
public final native Class<?> getClass()

//native方法，用于返回对象的哈希码，主要使用在哈希表中，比如JDK中的HashMap。
public native int hashCode()

//用于比较2个对象的内存地址是否相等，String类对该方法进行了重写用户比较字符串的值是否相等。
public boolean equals(Object obj)

//naitive方法，用于创建并返回当前对象的一份拷贝。一般情况下，对于任何对象 x，表达式 x.clone() != x 为true，x.clone().getClass() == x.getClass() 为true。
//Object本身没有实现Cloneable接口，所以不重写clone方法并且进行调用的话会发生CloneNotSupportedException异常。
protected native Object clone() throws CloneNotSupportedException

//返回类的名字@实例的哈希码的16进制的字符串。建议Object所有的子类都重写这个方法。
public String toString()

//native方法，并且不能重写。唤醒一个在此对象监视器上等待的线程(监视器相当于就是锁的概念)。如果有多个线程在等待只会任意唤醒一个。
public final native void notify()

//native方法，并且不能重写。跟notify一样，唯一的区别就是会唤醒在此对象监视器上等待的所有线程，而不是一个线程。
public final native void notifyAll()

//native方法，并且不能重写。暂停线程的执行。注意：sleep方法没有释放锁，而wait方法释放了锁 。timeout是等待时间。
public final native void wait(long timeout) throws InterruptedException

//多了nanos参数，这个参数表示额外时间（以毫微秒为单位，范围是 0-999999）。 所以超时的时间还需要加上nanos毫秒。
public final void wait(long timeout, int nanos) throws InterruptedException

//跟之前的2个wait方法一样，只不过该方法一直等待，没有超时时间这个概念
public final void wait() throws InterruptedException

//实例被垃圾回收器回收的时候触发的操作
protected void finalize() throws Throwable { }
```

#### 26. == 和 equles

* **(1) ==** : 它的作用是判断两个对象的地址是不是相等。即，判断两个对象是不是同一个对象(基本数据类型==比较的是值，引用数据类型==比较的是内存地址)。
* **(2) equals()** : 它的作用也是判断两个对象是否相等。但它一般有两种使用情况：
  * 情况 1：类没有覆盖 equals() 方法。则通过 equals() 比较该类的两个对象时，等价于通过“==”比较这两个对象。
  * 情况 2：类覆盖了 equals() 方法。一般，我们都覆盖 equals() 方法来比较两个对象的内容是否相等；若它们的内容相等，则返回 true (即，认为这两个对象相等)。

#### 27. 获取用键盘输入的两种方式

* 方法 1：通过 Scanner

  ```java
  Scanner input = new Scanner(System.in);
  String s  = input.nextLine();
  input.close();
  ```

* 方法 2：通过 BufferedReader

  ```java
  BufferedReader input = new BufferedReader(new InputStreamReader(System.in));
  String s = input.readLine();
  ```

#### 28. 文件和I/O流

Java 中 IO 流分为几种?

* 按照流的流向分，可以分为输入流和输出流；
* 按照操作单元划分，可以划分为字节流和字符流；
* 按照流的角色划分为节点流和处理流。
* InputStream/Reader: 所有的输入流的基类，前者是字节输入流，后者是字符输入流。
* OutputStream/Writer: 所有输出流的基类，前者是字节输出流，后者是字符输出流。