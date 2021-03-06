# Java并发编程
这一章关于一些多线程并发问题的解决，以及设计的一些同步技术的总结，大多为面试重要考点。
* [volatile](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/Concurrent/README.md#1-volatile)
* [CAS](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/Concurrent/README.md#2-cas)
* [集合类并发安全问题](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/Concurrent/README.md#3-aba%E9%97%AE%E9%A2%98)
## 1. volatile
volatile是Java虚拟机提供的**轻量级的同步机制**,它的特点有三点：
* 保证**可见性**
* 不保证**原子性**
* **禁止指令重排**
### 1.1 可见性
#### 1.1.1 什么可见性？
* 先讲讲JMM(Java内存模型)  
![JMM](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/Concurrent/imgs/JMM.png)  
* 可见性：当某个线程修改主内存值时，其他线程要很快知道该值被修改了（比如上图中Thread1将值a=3更新为a=4）  
#### 1.1.2 volatile可见性证明：  
* (1)代码中不用volatile修饰，用Thread1去修改主内存中共享变量的值，但Thread2不知道已修改；  
* (2)使用volatile修饰，线程1修改后，线程2获取的值即为修改后的值。  

### 1.2 原子性
#### 1.2.1 什么是原子性？
* 简单的讲：不可分割，完整性的操作集合。也就是说这些原子操作要么全执行成功，要么全部失败。
* volatile不保证原子性。
#### 1.2.2 怎保证原子性？
* 加synchronized（重量级锁）修饰，若只是解决num++;问题有点大材小用。
* 用Atomic-->AtomicInteger来解决num++;原子性问题。

### 1.3 指令重排
#### 1.3.1 什么是指令重排？
* 计算机运行某个程序，程序的运行时按指令运行，为了提高效率，编译器通常会对指令做重排一般分为以下三种:  
![InstructionRearrangement](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/Concurrent/imgs/recode.png)
#### 1.3.2 什么情况下会指令重排？
* (1)**单线程环境**，确保程序的最终执行结果和代码顺序执行的结果一致；
* (2)处理器在进行指令重排时必须考虑指令之间的**数据依赖性**，当无数据依赖时可进行指令重排；
* (3)**多线程环境下**，线程交替执行，因编译器优化重排的存在，两个线程使用的变量是否能保证一致性无法确定的，结果无法预判，故有时需要**禁止指令重排**。  

> **面试问题：什么场景下使用过volatile？**              
> 比如：**单例模式下DCL（Double check Lock 双端检锁机制）**            
> (1)DCL不一定线程安全，因为有指令重排的存在，加入volatile可禁止指令重排；            
> (2)由于指令重排，可能当一个线程访问instance不为null时，由于instance实例未必完成了初始化，这样就会产生线程不安全问题。                
## 2. CAS
**CAS**指比较和交换，`atomicInteger.compareAndSet(expect,update);` 若expect和主内存的变量值相同，则将值更新为update,否则返回false。**底层原理**是：  
* **自旋锁**
* **unsafe类**
### 2.1 unsafe类
* 1)unsafe类是CAS的核心类，由于Java无法直接访问底层系统，需要通过本地方法(native修饰)来访问，unsafe类相当于一个后门，基于该类可以直接操作特定内存的数据（unsafe类基本所有方法都是native修饰的，即unsaf类中的方法都直接调用操作系统底层资源执行相应的任务）。
* 2)变量valueoffset，表示该变量值在内存中的偏移地址，因为unsafe是通过偏移地址来获取数据的。
* 3)变量value用volatile修饰，保证多线程之间的内存可见性。
### 2.2 自旋锁

### 2.3 CAS的缺点
* (1)循环时间长，cpu开销大(因为自旋锁)
* (2)只能保证一个共享变量的原子操作
* (3)ABA问题
### 2.4 ABA问题
#### 2.4.1 什么是ABA问题
尽管线程A和B都可以进行CAS操作成功，但不代表这个过程就没有问题，有一种情况，在线程A操作过程中，可能线程B将内存共享变量的值修改过，只不过后面又修改回原始值了，这就是所谓的**ABA问题**。
#### 2.4.2 解决ABA问题
解决ABA问题-->原子引用+新机制，修改版本号（类似加时间戳），可以使用`tomicStampedReference.compareAndSet();`。
## 3. 集合类并发安全问题
> 线程不安全的集合类包括 ArrayList、HashMap、HashSet 等。
### 3.1 不安全问题（故障）
#### 3.1.1 故障现象
当发生故障会报`java.util.ConcurrentModificationException`异常。
#### 3.1.2 导致原因
`ConcurrentModificationException`是指并发修改异常，并发争抢资源，如一个线程在进行写操作，另一个线程抢夺写操作，导致数据不一致异常，也就是所谓的并发修改异常。
#### 3.1.3 解决方案
* 1)用vector<>();因为vector的add方法用`synchronized`修饰了。
* 2)使用Collections工具类，它提供了线程安全的集合类；比如`Collections.synchronizedList(new ArrayList<>());`,`Collections.synchronizedMap(new HashMap<>());`,`Collections.synchronizedSet(new HashSet<>());`等。
* 3)使用 `new CopyOnWriteArrayList<>();`或者`new CopyOnWriteArraySet<>();`
  * 底层原理实现：创建一个CopyOnWrite容器，即写时复制容器。当要往某个容器添加一个元素时，不直接往当前容器的Object[]中添加该元素，而是先复制一份，然后往复制的新容器里添加新元素，添加完成后，再将原容器的引用指向新容器。
### 3.2 HashSet
HashSet线程不安全，可以使用上面的解决方案，使用`CopyOnWriteArraySet`。
HashSet底层源码是由HashMap实现的：
```java
HashSet hs = new HashSet<>();
hs.add('a');
//上面操作，底层是hashMap.put('a',常量)；由于HashSet不关心value值，故可以设置一个常量值即可。
```
### 3.3 HashMap
HashMap也是线程不安全的，可使用`ConcurrentHashMap`分段锁来解决。
ConcurrentHashMap由数组结构Segments和HashEntry数组组成。segement是一种可重入锁(ReentrantLock)，扮演锁的角色，HashEntry则用于存储键值对数据。  
![HashMap](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/Concurrent/imgs/HashMap.png)   
> Java8抛弃了segment分段锁机制，利用CAS+Synchronized来保证并发安全，数据结构采用：数组+链表+红黑树。
