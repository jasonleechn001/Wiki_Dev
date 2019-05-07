# Wiki_Dev
## 并发编程模块
### volatile关键字
* volatile是解决内存可见性问题

  * 当多个线程操作共享数据时，彼此不可见，volatile修饰之后，每个线程都是直接对主存中的数据进行操作。

* 加volatile之后性能有所下降，但是比synchronized要高

  * 性能下降的原因：JVM底层有个优化叫重排序，用了volatile修饰后，不能进行重排序
  * volatile相比synchronized是一种轻量级的同步策略

* 与synchronized相比的差异

  * volatile不具备【互斥性】

  * volatile不能保证变量的【原子性】
  
### Atomic包下的原子操作
* java.util.concurrent.atomic包下提供了常用的原子变量，其有如下特点

  * 包装的值都是用volatile修饰，保证内存可见性

  * CAS（Compare-And-Swap）算法保证数据的原子性

    * CAS算法是硬件对并发操作共享数据的支持

    * CAS算法的三个操作数

      内存值：V

      预估值：A

      更新值：B

      当且仅当 V==A时，V=B；否则，将不做任何操作

    如果多个线程对主存中的数据进行修改时，有且只有一个线程能成功，CAS算法比原来的效率高的原因是：当不成功时它不会阻塞不会放弃CPU给他的执行权，会紧跟着立即再去尝试再去更新，所以说CAS算法要比普通同步锁的效率高很多。

    **缺点：当CAS算法更新失败时，我们自己要写失败的处理逻辑。**
