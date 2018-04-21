


# 基础

## 面向对象(OOP)

### 封装、继承和多态
* [《Java学习笔记——封装、继承和多态》](http://www.cnblogs.com/tomasman/p/6743732.html)

### 重载与重写
* [《重载与重写的区别》](https://blog.csdn.net/linzhaojie525/article/details/55213010)

## 语法

### finalize() 方法
* [《java finalize方法总结、GC执行finalize的过程》](https://blog.csdn.net/maoyeqiu/article/details/49562093)

* [《为什么在Java中不使用finalize()方法》](https://blog.csdn.net/maoyeqiu/article/details/49562093)
	* 不保证执行
	* 性能负担重。 

### foreach

#### foreach 原理

foreach之所以能工作，是因为这些集合类都实现了Iterable接口。

* [《java foreach实现原理》](https://www.cnblogs.com/vinozly/p/5465454.html)



### volatile
* [《Java并发编程：volatile关键字解析》](http://www.cnblogs.com/dolphin0520/p/3920373.html)
* [《举例解析Java中Volatile的作用》](https://blog.csdn.net/xilove102/article/details/52437581)
	* volatile 不能用于计数器
	* 对于volatile修饰的变量，jvm虚拟机只是保证从主内存加载到线程工作内存的值是最新的，两个线程及时用volatile关键字修改之后，还是会存在并发的情况。

* [《【Java线程】volatile的适用场景》](https://blog.csdn.net/vking_wang/article/details/9982709)
	* 比如：状态值；

###  transient
禁止序列化
* [《Java中的关键字 transient》](http://www.cnblogs.com/chenpi/p/6185773.html)


## 常用数据结构

### Object 对象

#### equals 和 hashCode
equals 满足等价关系：自反性、对称性、传递性。

重写了euqls方法的对象必须同时重写hashCode()方法，因为会用于 Hashtable, HashMap, HashSet 等对象中。

* [《一次性搞清楚equals和hashCode》](https://www.cnblogs.com/lulipro/p/5628750.html)

### wait()、notify()
* [《为什么wait()和notify()属于Object类》](https://www.cnblogs.com/lirenzhujiu/p/5927241.html)
	* 锁可以加在任意对象上。 

另外，wait 和 notify 方法不能被重写，因为声明的是 final 方法。

###  字符串

#### 字符串常量池的迁移
* [《Java中的字符串常量池详细介绍》](https://blog.csdn.net/u014134959/article/details/48805777)
* [《对于JVM中方法区，永久代，元空间以及字符串常量池的迁移和string.intern方法》](https://www.cnblogs.com/hadoop-dev/p/7169252.html)
* [《JVM内部细节之三：字符串及字符串常量池》](https://www.cnblogs.com/javaminer/p/3923484.html)
#### String.intern 方法

主要作用是将字符串副本复制（1.7后是地址）到常量区，主要用于节省内存。

* [《 几张图轻松理解String.intern()》](https://blog.csdn.net/soonfly/article/details/70147205)

### StringBuilder，StringBuffer
速度：StringBuilder > StringBuffer > String
线程安全：StringBuilder 不安全、StringBuilder 安全

String 直接拼接慢是因为需要反复申请内存，StringBuilder 和  StringBuilder 都是预分配内存。

* [《Java中的String，StringBuilder，StringBuffer三者的区别》](https://www.cnblogs.com/su-feng/p/6659064.html)
* [《StringBuilder剖析》](https://blog.csdn.net/qq_17505335/article/details/52806096)



### Integer

#### Integer 缓存
适用于 -127到 127 之间的整数，推荐有限使用原始类型。
* [《理解Java Integer的缓存策略》](http://www.importnew.com/18884.html)

### HashMap
* [《HashMap 的底层原理》](https://www.cnblogs.com/holyshengjie/p/6500463.html)
* [《java随笔——HashMap与红黑树》](https://www.cnblogs.com/liwei2222/p/8013367.html)
	* 在jdk1.8版本后，java对HashMap做了改进，在链表长度大于8的时候，将后面的数据存在红黑树中，以加快检索速度。

* [《HashMap的死循环解读》](https://www.cnblogs.com/dongguacai/p/5599100.html)
	* 多线程扩容导致。

**Hash Dos攻击**

* [《邪恶的JAVA HASH DOS攻击》](http://www.freebuf.com/articles/web/14199.html)
	* 利用JsonObjet 上传大Json，JsonObject 底层使用HashMap；不同的数据产生相同的hash值，使得构建Hash速度变慢，耗尽CPU。
* [《一种高级的DoS攻击-Hash碰撞攻击》](https://yq.aliyun.com/articles/92194?t=t1)
* [《关于Hash Collision DoS漏洞：解析与解决方案》](http://www.iteye.com/news/23939/)
* [《JEP 180: Handle Frequent HashMap Collisions with Balanced Trees》](http://openjdk.java.net/jeps/180)
	* Java 8 中对 HashMap做了增强，使用平衡树结构，提高hash冲突时的插入顺序。 

### HashTable
* [《Hashtable 的实现原理》](http://wiki.jikexueyuan.com/project/java-collection/hashtable.html)

HashMap 和 HashMap 区别：
* HashMap 的 key 和 value 都允许为 null，而 Hashtable 的 key 和 value 都不允许为 null
* Hashtable 方法是同步，而HashMap则不是。

**HashTable 已经被遗弃**

### ConcurrentHashMap

* [《从ConcurrentHashMap的演进看Java多线程核心技术》](http://www.jasongj.com/java/concurrenthashmap/)

* [《ConcurrentHashMap的size操作》](http://ifeve.com/concurrenthashmap/)
	* 因为在累加count操作过程中，之前累加过的count发生变化的几率非常小，所以ConcurrentHashMap的做法是先尝试2次通过不锁住Segment的方式来统计各个Segment大小，如果统计的过程中，容器的count发生了变化，则再采用加锁的方式来统计所有Segment的大小。 

### HashSet
内部使用 HashMap 来实现，Set 只存放在 HashMap 的Key中，Value使用一个常量。

* [《深入Java集合学习系列：HashSet的实现原理》](http://zhangshixi.iteye.com/blog/673143)

* [《HashSet （需要重写hashCode和equals方法）》](https://blog.csdn.net/dingjingchao/article/details/53150901)
	* 删除和判断元素是否存在，都是先判断hashCode 看看是否存在，若存在则继续equals(); 

### TreeMap
底层使用红黑树
* [《Java提高篇（二七）—–TreeMap》](http://cmsblogs.com/?p=1013)

### TreeSet
内部使用 TreeMap 来实现，好像就是 TreeMap 的一个马甲。
* [《java集合类深入分析之TreeMap/TreeSet篇》](http://shmilyaw-hotmail-com.iteye.com/blog/1836431)


### ArrayList
* [《Java ArrayList工作原理及实现》](http://www.importnew.com/18865.html)

### LinkedList
* [《Java中LinkedList原理解析》](http://www.codes51.com/article/detail_522924.html)

* [《Java中ArrayList和LinkedList区别》](https://www.cnblogs.com/soundcode/p/6294174.html)

### BitSet
* [《Java Bitset类》](http://www.runoob.com/java/java-bitset-class.html)
* [《Java BitSet（位集）》](https://blog.csdn.net/caiandyong/article/details/51581160)

## 异常

### Exception 和 Error
* [《ERROR与EXCEPTION的区别》](https://blog.csdn.net/sjtu_chenchen/article/details/49658749)


### RuntimeException

不需要强制 try...catch，不需要强制 throw，顶层调用层未知。

* [《5个常见的RuntimeException》](https://blog.csdn.net/xiuye2015/article/details/48138977)

* [《常见的几种RuntimeException》](https://blog.csdn.net/qq635785620/article/details/7781026)

### RuntimeException 和 Exception
* [《RuntimeException和Exception区别》](https://www.cnblogs.com/jtlgb/p/5985120.html)

## 常用工具类

### Optional
便于链式调用

* [《Java8 如何正确使用 Optional》](http://www.importnew.com/26066.html)

## 设计模式

### Double Check Lock (DCL)

### 集合框架

#### Collections
##### Collections.synchronized 系列方法
* [《Java Collections.synchronizedMap方法分析》](https://blog.csdn.net/Cantus_hjk/article/details/48435481)
	* 加锁的代理模式。 
##### Collections.sort 

* [《Collections中sort()和Arrays中的sort方法分析》](https://blog.csdn.net/rebirth_love/article/details/51447829)

 * [《Java中Collections.sort()和Arrays.sort()所采用的排序算法》](https://www.cnblogs.com/merru/articles/4666493.html)
	* Collections.sort算法调用的是合并排序。
	* Arrays.sort() 采用了2种排序算法 -- 基本类型数据使用快速排序法，对象数组使用归并排序。


## 注解

* [《注解Annotation实现原理与自定义注解例子》](https://www.cnblogs.com/acm-bingzi/p/javaAnnotation.html)

## JVM

### 内存模型

* [《Java内存数据模型》](https://www.cnblogs.com/wyq178/p/6915952.html)
	* 线程私有内存：程序计数器（无内存溢出，也叫PC 寄存器）、虚拟机栈、本地方法栈。
	* Java虚拟机栈：操作方法调用相关信息的栈帧；每个线程有一个私有的栈。
	* 本地方法栈： Native 方法发执行的栈帧。
	* 堆：存放对象；包括：新生代、老年代、Eden空间、From survivor空间、To Survior空间；GC 的主要区域；线程间共享。
	* 方法区：存放类信息、常量、静态变量等；也会被GC；运行时常量池在方法区中，比如字符串和符号引用；只有 Hotspot 才有。
* [《Jvm内存模型和内存分配》](https://www.cnblogs.com/fubaizhaizhuren/p/4976839.html)
* [《Java内存分配之堆、栈和常量池》](https://www.cnblogs.com/SaraMoring/p/5687466.html)

### Java 8 中的元空间

* [《Java8内存模型—永久代(PermGen)和元空间(Metaspace)》](http://www.cnblogs.com/paddix/p/5309550.html)
	* Java 8 中完全移除了 PermGen 空间，并用 Metaspace 取代。 
	* 元空间并不在虚拟机中，而是使用本地内存，默认没有限制。

* [《JDK8-废弃永久代（PermGen）迎来元空间（Metaspace）》](https://www.cnblogs.com/dennyzhangdd/p/6770188.html)
	* 移除官方解释：移除永久代是为融合HotSpot JVM与 JRockit VM而做出的努力，因为JRockit没有永久代，不需要配置永久代。

* [《Java 8的元空间》](https://blog.csdn.net/yongfeng596/article/details/25836111)
	* 省掉了GC扫描及压缩的时间。
	* 减少碎片的策略。
	* 不会单独回收某个类。

### 堆空间中内存的迁移
* [《Java系列笔记(3) - Java 内存区域和GC机制》](http://www.cnblogs.com/zhguang/p/3257367.html)

* [《为什么新生代内存需要有两个Survivor区？》](https://www.cnblogs.com/jimmy-muyuan/p/8734641.html)
	* Survivor 空间避免老年代空间迅速被占满，从而引起FullGC。
	* 两个 Survivor 空间避免内存碎片。


### 引用类型
* [《强引用、弱引用、软引用、虚引用》](http://www.open-open.com/lib/view/open1429609953963.html)
	* 引用强度：  强引用  >  软引用  >  弱引用  >  虚引用。
	* 回收时机：强引用不回收；软引用内存不足时回收；弱引用GC后回收；
	* 应用：强引用用于一般对象；软引用、弱引用用于本地缓存；虚引用的主要作用是跟踪对象被垃圾回收的状态；


### 指令指令重排 与  happens-before 规则 

* [《从JVM并发看CPU内存指令重排序(Memory Reordering)》](https://blog.csdn.net/kobejayandy/article/details/9751445)
	* 背景是由于CPU cache 和 主存的速度差造成的重排。 
* [《深入理解Java内存模型（二）——重排序》](http://www.infoq.com/cn/articles/java-memory-model-2/)

 happens-before 用于JVM编译优化时指令重拍的直到原则

* [《通俗易懂讲解happens-before原则》](https://blog.csdn.net/u010031673/article/details/48153797)
* [《死磕Java并发：Java内存模型之happens-before》](https://blog.csdn.net/GarfieldEr007/article/details/56513303)
* [《Java内存模型详解》](http://www.360doc.com/content/09/1026/08/397210_7863338.shtml)

* [《不得不提的volatile及指令重排序(happen-before)》](https://www.cnblogs.com/xll1025/p/6486170.html)
	* volatile的第一条语义是保证线程间变量的可见性。
	* volatile的第二条语义：禁止指令重排序。

### 类加载
三个系统加载器：Bootstrap ClassLoader（C++实现，JVM内置）、ExtClassLoader、AppClassLoader
双亲委派：优先使用上一层(父加载器)来加载类，作用是为了是类型统一，简单说就是先从爷爷找，再从爹找。

* [《JVM 类加载机制详解》](http://www.importnew.com/25295.html)
* [《双亲委派模型》](https://blog.csdn.net/p10010/article/details/50448491)


### JIT

### HotSpot，JRockit，OpenJDK，J9

* OpenJDK：openjdk是jdk的开放原始码版本，以GPL协议的形式放出。在JDK7的时候，openjdk已经成为jdk7的主干开发，sun jdk7是在openjdk7的基础上发布的；

* HotSpot 提起HotSpot VM,相信所有Java程序员都知道,它是Sun JDK和OpenJDK中所带的虚拟机。 
* Oracle JRockit JVM 是业界性能最高的 Java 虚拟机。

* [《OpenJDK和JDK区别》](http://fgh2011.iteye.com/blog/1771649)

## 垃圾回收

### 垃圾回收算法

* [《图解JVM垃圾回收算法》](https://blog.csdn.net/wen7280/article/details/54428387)
	* 引用计数法：为每个对象创建一个计数器，实现简单，但无法处理循环引用问题，容易OOM，JVM未采用。
	* 标记清除法：标记清除法是现代垃圾回收算法的思想基础，记所有从根节点开始的可达对象，因此未被标记的对象就是未被引用的垃圾对象。
		* 两个阶段：标记阶段和清除阶段。
		* 优点：可以解决循环引用的问题。
		* 缺点：内存分配不连续，容易产生空间碎片。
	* 复制算法：将内存分为两份，一次只使用一个，一个满时将，将存货对象拷贝到另一份中，其余则清除，适用于存活存活对象少，垃圾对象对的情况，比如新生代。
		* 优点：没有碎片。
		* 缺点：系统内存空间折半，只用一半。
		* 在java中的新生代串行垃圾回收器中，使用了复制算法的思想。
	* 标记压缩算法：应用标记清除法之后，再进行一次碎片整理。
	* 分代算法：新生代用复制算法、老年代用标记算法。
	* 分区算法：整个堆空间划分为连续的不同小区间、每一个小区间都独立使用，独立回收。
		* 优点：可以控制一次回收多少个小区间、避免一次GC整个空间。

### 垃圾回收器

* [《垃圾回收算法与 JVM 垃圾回收器综述》](http://www.cnblogs.com/smyhvae/p/4810168.html)
	* Serial GC：串行GC处理器，-XX：+UseSerialGC， Client 模式下运行时，它是默认的垃圾回收器。
		* 新生代使用复制算法。
		* 老年代使用是标记-压缩算法。
		* 在堆空间较大的情况下，GC时间比较长，几秒甚至更长。 
	* ParNew GC：并行回收器是工作在新生代的垃圾回收器，它只简单地将串行回收器多线程化。它的回收策略、算法以及参数和串行回收器一样。在收集过程中，应用程序会全部暂停。
	* Parallel GC：尽可能降低用户线程停顿时间，提高吞吐量。
		* 使用 -XX:+UseParallelOldGC 可以在新生代和老生代都使用并行回收回收器。
		* 新生代使用的复制算法，老年代使用标记压缩算法。
	* CMS：Concurrent Mark-Sweep ，工作在老年带上，和用户线程同时工作，目标是获得更短的停顿时间。
		* CMS回收器不再采用简单的指针指向一块可用堆空间来为下次对象分配使用。而是把一些未分配的空间汇总成一个列表，当 JVM 分配对象空间的时候，会搜索这个列表找到足够大的空间来存放住这个对象。
		* CMS不会在老年代满的时候才开始收集。相反，它会尝试更早的开始收集，默认是当老年代使用68%的时候，CMS就开始行动了。 – XX:CMSInitiatingOccupancyFraction =n 来设置这个阀值。
		* 在若干次GC后，CMS必须进行一次碎片整理。
		* 步骤：初始标记（STW）、并发标记、并发预清理、重新标记(STW)、并发清理、并发重置。
	* G1： JDK 1.7 中引入，用于取代CMS。
		* 没有物理上隔断新生代与老生代，但也属于分代垃圾回收期，切兼顾两代。
		* G1 GC 首先将堆分为大小相等的 Region，避免全区域的垃圾收集。 
		* 可预见模型：G1会选择适当的区域进行收集，确保停顿时间不超过用户指定时间。
		* 过程：初始标记（STW）、并发标记、最终标记（STW）、筛选回收(在指定时间内回收)。


* [《JVM中的G1垃圾回收器》](http://www.importnew.com/15311.html)

## 序列化

### Serializable 作用
* [《接口java.io.Serializable的用处 》](https://blog.csdn.net/chenjie19891104/article/details/4398647)



## 反射

* [《Java 反射 使用总结》](https://www.cnblogs.com/zhaoyanjun/p/6074887.html)
	* 用途：在运行时判断任意一个对象所属的类；
	* 在运行时构造任意一个类的对象；
	* 在运行时判断任意一个类所具有的成员变量和方法；
	* 在运行时调用任意一个对象的方法；
		 生成动态代理。	 

* [《Java动态代理之JDK实现和CGlib实现（简单易懂）》](http://www.cnblogs.com/ygj0930/p/6542259.html)
	* 静态代理是需要显示关联。
	* 动态代理通过 InvocationHandler 的实现类实例进行动态关联，JDK自带功能。
	* CGlib 无需通过接口就可以修改原始类方法，更加灵活。CGlib动态代理是通过继承业务类，生成的动态代理类是业务类的子类，通过重写业务方法进行代理；

## 垃圾回收

### GC 算法

## 内存分区

## 引用类型
强、弱、软、

## 类加载


# 多线程、并发

## 并行与并发
* [《并发与并行的区别》](https://blog.csdn.net/java_zero2one/article/details/51477791)

## 锁 & 同步

### synchronized
* [《synchronized 作用在普通方法与静态方法的区别》](https://www.cnblogs.com/guiqulai/articles/7342006.html)

* [《Java中synchronized的实现原理与应用》](https://blog.csdn.net/u012465296/article/details/53022317)

* [《详解synchronized与Lock的区别与使用》](https://blog.csdn.net/u012403290/article/details/64910926)

### CopyOnWrite容器

可以对CopyOnWrite容器进行并发的读，而不需要加锁。CopyOnWrite并发容器用于读多写少的并发场景。比如白名单，黑名单，商品类目的访问和更新场景，不适合需要数据强一致性的场景。

* [《JAVA中写时复制(Copy-On-Write)Map实现》](https://www.cnblogs.com/hapjin/p/4840107.html)
* [《聊聊并发-Java中的Copy-On-Write容器》](https://blog.csdn.net/a494303877/article/details/53404623)

### ReadWriteLock

* [《ReadWriteLock场景应用》](https://www.cnblogs.com/liang1101/p/6475555.html)
	* 缓存处理



### AQS

AQS - AbstractQueuedSynchronizer，AQS定义了一套多线程访问共享资源的同步器框架，许多同步类实现都依赖于它，如常用的ReentrantLock/Semaphore/CountDownLatch。

* [《Java并发之AQS详解》](https://www.cnblogs.com/waterystone/p/4920797.html)
	* 通过 state 字段的增减控制锁的添加和释放。

### Condition条件
Condition 条件，用于替代传统 Object的 wait()、notify() 实现线程间的协作。

* [《Condition使用总结》](https://blog.csdn.net/heyutao007/article/details/49889849)
* [《java Condition条件变量的通俗易懂解释、基本使用及注意点》](https://www.cnblogs.com/zhjh256/p/6389168.html)
* [《java并发编程之Condition》](https://www.jianshu.com/p/be2dc7c878dc)
* [《入门AQS锁 - Condition与LockSupport》](https://www.jianshu.com/p/1add173ea703)

### CountDownLatch

是一种共享锁、为0时才可以继续执行，内部使用AQS，state记录数量。
主线程使用await，子线程使用 countDown.
场景举例: 分批读取数据。

* [《java共享锁实现原理及CountDownLatch解析》](https://blog.csdn.net/yanyan19880509/article/details/52349056)
* [《什么时候使用CountDownLatch》](http://www.importnew.com/15731.html)


### CyclicBarrier

子线程使用 await，全部await 时再执行下一步。
场景举例：一起去吃饭。

* [《并发工具类（二）同步屏障CyclicBarrier》](http://ifeve.com/concurrency-cyclicbarrier/)
	* 与 CountDownLatch 区别：CountDownLatch 一次性，CyclicBarrier 可以使用 reset 重置。；CyclicBarrier 方法更多，适合复杂场景。

* [《深入浅出java CyclicBarrier》](https://www.jianshu.com/p/424374d71b67)
	* 内部使用 ReentrantLock。

### Semaphore
也是是一个共享锁，内部使用 AQS，分为 "公平信号量"和"非公平信号量"。

* [《Java多线程系列--“JUC锁”11之 Semaphore信号量的原理和示例》](http://www.cnblogs.com/skywang12345/p/3534050.html)

###  Exchanger

* [《Exchanger的工作原理及实例》](https://blog.csdn.net/carson0408/article/details/79477280)

* [《Java并发编程中Exchanger的用法》](https://blog.csdn.net/sinat_36246371/article/details/53873693)

## 多线程

### Callable、Future 和 FutureTask
* [《Java多线程编程：Callable、Future和FutureTask浅析（多线程编程之四）》](https://blog.csdn.net/javazejian/article/details/50896505)

### ThreadLocal 
原理 + 应用场景

* [《ThreadLocal可能引起的内存泄露》](https://www.cnblogs.com/onlywujun/p/3524675.html)
* [《使用ThreadLocal不当可能会导致内存泄露》](http://ifeve.com/%E4%BD%BF%E7%94%A8threadlocal%E4%B8%8D%E5%BD%93%E5%8F%AF%E8%83%BD%E4%BC%9A%E5%AF%BC%E8%87%B4%E5%86%85%E5%AD%98%E6%B3%84%E9%9C%B2/)

### 线程池
* [《java并发编程—— 线程池原理 详解 ThreadPoolExecutor》](https://blog.csdn.net/lemon89/article/details/50987937)

* [《Java四种线程池的使用》](http://cuisuqiang.iteye.com/blog/2019372)
	* newCachedThreadPool（变长）、newFixedThreadPool(定长)、newScheduledThreadPool(定长可调度，可调度)、newSingleThreadExecutor(单线程)。




## 并发工具包

### ConcurrentLinkedQueue

使用 CAS 方式实现无阻塞。

* [《并发队列-无界非阻塞队列 ConcurrentLinkedQueue 原理探究》](http://www.importnew.com/25668.html)
* [《ConcurrentLinkedQueue的实现原理分析》](http://www.infoq.com/cn/articles/ConcurrentLinkedQueue)


## Fork/Join

* [《Fork/Join框架介绍》](http://www.infoq.com/cn/articles/fork-join-introduction)



## NIO

### zerocopy 





双亲委派。
OSGI

## Java 版本

### Java 8 新特性

* [《java8新特性详解》](https://blog.csdn.net/liubenlong007/article/details/62039628)

永久代，元空间。
https://www.cnblogs.com/hadoop-dev/p/7169252.html

### Java 9

Java 10 新特性

## 扩展功能
### SPI

* [《java中的SPI机制》](https://blog.csdn.net/sigangjun/article/details/79071850)

# Web 

## Servlet

* [《Servlet 生命周期》](http://www.runoob.com/servlet/servlet-life-cycle.html)
* [《Servlet的生命周期》](https://blog.csdn.net/liushengmeng/article/details/7978462?locationNum=7&fps=1)
* [《Servlet开发(一)》](https://www.cnblogs.com/xdp-gacl/p/3760336.html)

## Spring

* [《Spring中的beanFactory和ApplicationContext的有什么区别和关联》](https://blog.csdn.net/judyfun/article/details/44172641)

### Spring Bean 

#### 生命周期
* [《Spring中Bean的生命周期是怎样的？》](https://www.zhihu.com/question/38597960)

#### 作用域
* [《Spring中Bean的五个作用域》](https://blog.csdn.net/u011468990/article/details/49995865)

### 事务

* [《Spring事务管理（详解+实例）》](https://blog.csdn.net/trigl/article/details/50968079)
* [《JDK动态代理给Spring事务埋下的坑》](https://blog.csdn.net/crystalqy/article/details/79098733)

### 注解
* [《Spring注解@Resource和@Autowired区别对比》](https://www.cnblogs.com/think-in-java/p/5474740.html)
	* Autowired 只按照 byType注入。@Resource 默认按照ByName，也可以用 type。

### AOP

* [《Spring3：AOP》](http://www.cnblogs.com/xrq730/p/4919025.html)


### SpringMVC
* [《Spring MVC 入门示例讲解》](http://www.importnew.com/15141.html)

* [《SpringMVC运行原理》](http://www.codes51.com/article/detail_1723674.html)
	* DispatcherServlet 负责接收请求，然后分发；DispatcherServlet 是调度核心。
	* 找 Handler Mapping 找到对应的 Handler，然后交给处理器(Controller) 处理。
	* Handler(Controller) 处理完成后返回 ModelAndView 给 DispatcherServlet。
	* DispatcherServlet 再根据  ModelAndView 和 ViewResolver
	* DispatcherServlet 最后展示最终的View ，并返回给用户。

* [《第三章 DispatcherServlet详解 ——跟开涛学SpringMVC》](http://jinnianshilongnian.iteye.com/blog/1602617)


### SpringBoot

# 开源框架

## 数据库连接池

* [《主流Java数据库连接池比较与开发配置实战》](https://blog.csdn.net/fysuccess/article/details/66972554)

## RPC

### Dubbo


# JVM 语言

Kotlin

Groovy


## Spring

# 调试

# 工具

## JDK 工具 
*  [《JVM性能调优监控工具jps、jstack、jmap、jhat、jstat、hprof使用详解》](https://my.oschina.net/feichexia/blog/196575)

## 常用的 JDK 包
* [《JDK中常用包及其类和功能详细剖析》](https://blog.csdn.net/u011915230/article/details/53113525)

# 资源

## 在线文档、教程

* [《简明Java手册》](http://www.runoob.com/java/java-tutorial.html)

## 参考书

* 《深入理解Java虚拟机》[京东](https://union-click.jd.com/jdc?d=ccOmG5) [淘宝](https://s.taobao.com/search？q=%E6%B7%B1%E5%85%A5%E7%90%86%E8%A7%A3Java%E8%99%9A%E6%8B%9F%E6%9C%BA) 

* 《Java编程思想》[京东](https://union-click.jd.com/jdc?d=s2uN52) [淘宝](https://s.taobao.com/search?q=Java编程思想) 
