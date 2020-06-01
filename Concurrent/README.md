# Java并发编程
这一章关于一些多线程并发问题的解决，以及设计的一些同步技术的总结，大多为面试重要考点。
* [volatile](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/Concurrent/README.md#volatile)
* [CAS](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/Concurrent/README.md#cas)
* [ABA问题](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/Concurrent/README.md#aba%E9%97%AE%E9%A2%98)
# 1. volatile
volatile是Java虚拟机提供的**轻量级的同步机制**,它的特点有三点：
* 保证**可见性**
* 不保证**原子性**
* **禁止指令重排**
## 1.1 可见性
#### 1.1.1 什么是可见性？
* JMM(Java内存模型)  
![JMM](https://github.com/Hi-world-DF/Interview-knowledge-points/blob/master/Concurrent/imgs/JMM.png)  
> 可见性：当某个线程修改主内存值时，其他线程要很快知道该值被修改了（比如上图中Thread1将值a=3更新为a=4）  
> 证明volatile的可见性：  
> (1)代码中不用volatile修饰，用Thread1去修改主内存中共享变量的值，但Thread2不知道已修改；  
> (2)使用volatile修饰，线程1修改后，线程2获取的值即为修改后的值。  
# 2. CAS

# 3. ABA问题
