### Java 并发编程实战
本书能够全面建立起 Java 并发设计的理论知识架构，具有很好的研读意义，但是有些知识不够深入。  
阅读后的主要观察点为：  
1. 线程的安全性（正确性，原子性，内存可见性）与 活跃性（死锁，活锁，饥饿）  
2. 同步容器（ Vector,HashTable 具体实现中，采用方法级别的 synchronized ，串行化单个操作，对于复合操作（eg.遍历）依旧存在并发问题）  
3. 并发容器（ ConcurrentHashMap，CopyOnWriteArrayList 采用锁分解,锁分段，非阻塞方法等，具有更高的并发性）  
4. 同步工具类（闭锁（countDownLatch），信号量（Semaphore），栅栏（CyclicBarrier））
5. 内置锁（Synchronized）与 Lock 体系，内置锁不适用时采用 Lock 体系（ReentrantLock 可以实现 synchronized 功能）  
6. 生产者与消费者模式，Executor 体系
7. cas 与 锁，在竞争度不高的情况下 cas 具有更好的性能，竞争高的情况下锁更好解决。cas 与 非阻塞同步 与 原子变量  
####  推荐章节： 2-8，10-11，13-16，配合 Java 并发编程之美的源码解析更优  
