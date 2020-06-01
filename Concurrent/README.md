# Java并发编程
这一章关于一些多线程并发问题的解决，以及设计的一些同步技术的总结，大多为面试重要考点。
* [volatile](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/Concurrent/README.md#1-volatile)
* [CAS](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/Concurrent/README.md#2-cas)
* [ABA问题](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/Concurrent/README.md#3-aba%E9%97%AE%E9%A2%98)
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


## 3. ABA问题

