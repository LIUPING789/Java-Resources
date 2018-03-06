# Java-Resources
## Java 基础及Java Web 相关资料

*  __Http1与Http2的区别?__

   1､HTTP2使用的是二进制传送，HTTP1.X是文本(字符串)传送。 大家都知道HTTP1.X使用的是明文的文本传送，而HTTP2使用的是二进制传送，二进制传送的单位是帧和      流。帧组成了流，同时流还有流ID标示，通过流ID就牵扯出了第二个区别。

   2､HTTP2支持多路复用。因为有流ID，所以通过同一个http请求实现多个http请求传输变成了可能，可以通过流ID来标示究竟是哪个流从而定位到是哪个http请求。

   3､HTTP2头部压缩。HTTP2通过gzip和compress压缩头部然后再发送，同时客户端和服务器端同时维护一张头信息表，所有字段都记录在这张表中，这样后面每次传输只      需要传输表里面的索引Id就行，通过索引ID就可以知道表头的值了。

   4､HTTP2支持服务器推送。HTTP2支持在客户端未经请求许可的情况下，主动向客户端推送内容
   
  * __String能被继承吗?  为什么?__
  
    1､不可以，因为String类有final修饰符，而final修饰的类是不能被继承的，实现细节不允许改变。
    
  * __什么是深拷贝和浅拷贝?__
    
    一般步骤是(浅复制):

    1､被复制的类需要实现Clonenable接口(不实现的话在调用clone方法会抛出CloneNotSupportedException异常) 该接口为标记接口(不含任何方法)

    2､覆盖clone()方法，访问修饰符设为public。方法中调用super.clone()方法得到需要的复制对象，(native为本地方法)

    3､总结:浅拷贝是指在拷贝对象时，对于基本数据类型的变量会重新复制一份，而对于引用类型的变量只是对引用进行拷贝，没有对引用指向的对象进行拷贝。而深拷贝       是指在拷贝对象时，同时会对引用指向的对象进行拷贝。区别就在于是否对 对象中的引用变量所指向的对象进行拷贝。
    
 * __Java常见的几个运行时异常?__
 
   1、ClassCastException

   2、NullPointerException

   3、ArrayIndexOutOfBoundsException

   4、NumberFormatException

   5、NoClassDefFoundException

   6、.....
* __JDK引入泛型是解决什么问题的?__

   Java语言引入泛型的好处是安全简单。 在Java SE 1.5之前，没有泛型的情况的下，通过对类型Object的引用来实现参数的“任意化”，“任意化”带来的缺点是要做显式的强制类型转换，而这种转换是要求开发者对实际参数类型可以预知的情况下进行的。对于强制类型转换错误的情况，编译器可能不提示错误，在运行的时候才出现异常，这是一个安全隐患。 泛型的好处是在编译的时候检查类型安全，并且所有的强制转换都是自动和隐式的,提高代码的重用率。

* __谈谈hashCode与equals之间的关系?__

   因为如果只覆盖了equals而没有覆盖hashCode, 则两个不同的instance a和b虽然equals结果(业务逻辑上)相等,但却会有不同的hashcode,这样hashmap里面会同时存在a和b,而实际上我们需要hashmap里面只能保存其中一个,因为从业务逻辑方向看它们是相等的。 equals方法和hashCode方法如果不同时按你自己逻辑覆盖的话，HashMap就会出问题。比如你只覆盖了equals方法而没有覆盖hashCode方法，那么HashMap在第一步寻找链表的时候会出错，有同样值的两个对象Key1和Key2并不会指向同一个链表或桶，因为你没有提供自己的hashCode方法，那么就会使用Object的hashCode方法，该方法是根据内存地址来比较两个对象是否一致，由于Key1和Key2有不桶的内存地址，所以会指向不同的链表，这样HashMap会认为key2不存在，虽然我们期望Key1和Key2是同一个对象;反之如果只覆盖了hashCode方法而没有覆盖equals方法，那么虽然第一步操作会使Key1和Key2找到同一个链表，但是由于equals没有覆盖，那么在遍历链表的元素时，key1.equals(key2)也会失败(事实上Object的equals方法也是比较内存地址)，从而HashMap认为不存在Key2对象，这同样也是不正确的。
   
* __谈谈反射机制？__

   1.何谓反射机制。

   JAVA反射机制是在运行状态中，对于任意一个类，都能够知道这个类的所有属性和方法;对于任意一个对象，都能够调用它的任意一个方法;这种动态获取的信息以及动态调用对象的方法的功能称为java语言的反射机制。

   2.反射机制如何实现。

   Java程序在运行时，Java运行时系统一直对所有的对象进行所谓的运行时类型标识。这项信息纪录了每个对象所属的类。虚拟机通常使用运行时类型信息选准正确方法去执行，用来保存这些类型信息的类是Class类。也就是说，ClassLoader找到了需要调用的类时(java为了调控内存的调用消耗，类的加载都在需要时再进行，很抠但是很有效)，就会加载它，然后根据.class文件内记载的类信息来产生一个与该类相联系的独一无二的Class对象。该Class对象记载了该类的字段，方法等等信息。以后jvm要产生该类的实例，就是根据内存中存在的该Class类所记载的信息(Class对象应该和我所了解的其他类一样会在堆内存内产生、消亡)来进行。而java中的Class类对象是可以人工自然性的(也就是说开放的)得到的(虽然你无法像其他类一样运用构造器来得到它的实例，因为Class对象都是jvm产生的。不过话说回来，客户产生的话也是无意义的)，而且，更伟大的是，基于这个基础，java实现了反射。

  3.获取Class对象有三种方式:

  1).通过Object类的getClass()方法。

  2).通过Class类的静态方法——forName()来实现。

  3).如果T是一个已定义的类型的话，在java中，它的.class文件名:T.class就代表了与其匹配的Class对象。
  
*  __常用的JVM设置参数都有哪些?__

    #### 整体考虑堆大小
    -Xms3550m， 初始化堆大小。通常情况和-Xmx大小设置一样，避免虚拟机频繁自动计算后调整堆大小。-Xmx3550m，最大堆大小。
   
   #### 新生代
   -xmn2g，新生代大小。Sun官方推荐配置为整个堆的3/8。-XX:SurvivorRatio=8。Eden和Survivor的比值。

   #### 老年代
   老年代=整个堆大小-新生代-永久代

   #### 永久代
   -XX:Permsize=512m,设置永久代初始值。-XX:MaxPermsize=512m，设置永久代的最大值。
   注:Java8没有永久代说法，它们被称为元空间,-XX:MetaspaceSize=N

   #### 考虑本机直接内存
   -XX:MaxDirectMemorySize=100M。默认与Java堆大最大值(-Xmx)

   #### 考虑虚拟机栈
   每个线程池的堆栈大小。在jdk5以上的版本，每个线程堆栈大小为1m，jdk5以前的版本是每个线程池大小为256k。一般设置256k。 -Xss256K。

......

 [更多JVM参数配置](https://www.cnblogs.com/edwardlauxh/archive/2010/04/25/1918603.html)
 
* __HashMap和HashTable的区别?__

   1、继承的父类不同。 Hashtable继承自Dictionary类，而HashMap继承自AbstractMap类。但二者都实现了Map接口。

   2、线程安全性不同。Hashtable 中的方法是Synchronize的，而HashMap中的方法在缺省情况下是非Synchronize的。在多线程并发的环境下，可以直接使用               Hashtable，不需要自己为它的方法实现同步，但使用HashMap时就必须要自己增加同步处理。(结构上的修改是指添加或删除一个或多个映射关系的任何操作;仅改变       与实例已经包含的键关联的值不是结构上的修改。)这一般通过对自然封装该映射的对象进行同步操作来完成。如果不存在这样的对象，则应该使用                     Collections.synchronizedMap 方法来“包装”该映射。最好在创建时完成这一操作，以防止对映射进行意外的非同步访问。

   3、是否提供contains方法。 HashMap把Hashtable的contains方法去掉了，改成containsValue和containsKey，因为contains方法容易让人引起误解。Hashtable       则保留了contains，containsValue和containsKey三个方法，其中contains和containsValue功能相同。
   
   4、key和value是否允许null值。 Hashtable中，key和value都不允许出现null值。但是如果在Hashtable中有类似put(null,null)的操作，编译同样可以通过，因       为key和value都是Object类型，但运行时会抛出NullPointerException异常，这是JDK的规范规定的。HashMap中，null可以作为键，这样的键只有一个，可以有       一个或多个键所对应的值为null。

   5、两个遍历方式的内部实现上不同。 Hashtable、HashMap都使用了 Iterator。而由于历史原因，Hashtable还使用了Enumeration的方式 。

   6、hash值不同。哈希值的使用不同，HashTable直接使用对象的hashCode。而HashMap重新计算hash值。

   7、内部实现使用的数组初始化和扩容方式不同。HashTable在不指定容量的情况下的默认容量为11，而HashMap为16，Hashtable不要求底层数组的容量一定要为2的整       数次幂，而HashMap则要求一定为2的整数次幂。Hashtable扩容时，将容量变为原来的2倍加1，而HashMap扩容时，将容量变为原来的2倍。
  
  * __ArrayList和Vector的主要区别?__
  
   1､Vector是线程安全的，源码中有很多的synchronized可以看出，而ArrayList不是。导致Vector效率无法和ArrayList相比;

   2､ArrayList和Vector都采用线性连续存储空间，当存储空间不足的时候，ArrayList默认增加为原来的50%，Vector默认增加为原来的一倍;3.Vector可以设置            capacityIncrement，而ArrayList不可以，从字面理解就是capacity容量，Increment增加，容量增长的参数。
   
 * __List是有序的吗?__
   
   有序可重。有序或无序是指是否按照其添加的顺序来存储对象。List 是按照元素的添加顺序来存储的。
   
 * __ArrayList和LinkedList的区别?分别用在什么场景?__
  
   1､ArrayList是最常用的List实现类，内部是通过数组实现的，它允许对元素进行快速随机访问。数组的缺点是每个元素之间不能有间隔，当数组大小不满足时需要增加      存储能力，就要讲已经有数组的数据复制到新的存储空间中。当从ArrayList的中间位置插入或者删除元素时，需要对数组进行复制、移动、代价比较高。因此，它适      合随机查找和遍历，不适合插入和删除。

   2､LinkedList是用链表结构存储数据的，很适合数据的动态插入和删除，随机访问和遍历速度比较慢。另外，他还提供了List接口中没有定义的方法，专门用于操作表头      和表尾元素，可以当作堆栈、队列和双向队列使用。
   
 *  __ArrayList默认大小是多少，是如何扩容的?__
 
    ArrayList默认构造的容量为10，没错。 因为ArrayList的底层是由一个Object[]数组构成的，而这个Object[]数组，默认的长度是10，所以有的文章会说             ArrayList长度容量为10。然而你所指的size()方法，指的是“逻辑”长度。ArrayList默认size()是0。ArrayList之后扩容会按照1.5倍增长。
    
 * __List是线程安全的吗?如果要线程安全要怎么做?__
 
   不安全。实现线程安全方法:

   1､使用synchronized关键字。

   2､使用Collections.synchronizedList()。
   
*  __怎么给List排序?__

   1､实体类自己实现比较。实现comparable接口:public interface Comparable ，里面就一个方法声明:public int compareTo(T o);用Java中提供的对集合进行操      作的工具类Collections，其中的sort方法

   2､Collections提供的第二种排序方法sort(List list, Comparator c)。
   
 * __Arrays.asList方法后的List可以扩容吗?__
 
    不能！
    原因是Arrays.asList方法返回的ArrayList是继承自AbstractList同时实现了RandomAccess和Serializable接口。如果改变长度会抛出                           UnsupportedOperationException异常。
    
*  __List和Array之间如何互相转换?__

      list -> array =list.toArray()

      array -> list = Arrays.asList()

      迭代器循环法。
      
  *  __Collection集合接口和Map接口有什么关系?__
  
     都是集合框架体系，Collection定义的是单列集合。Map定义的是双列集合.
     
  *  __HashMap是线程安全的吗?线程安全的Map都有哪些?性能最好的是哪个?__
  
      HashMap不安全，线程安全的Map有hashTable、ConcurrentHashMap、通过Collections.synchronizedMap()。性能最好的是ConcurrentHashMap。通过分段锁来    实现线程安全，默认并发数是16，扩容是按16的倍数增长。hashMAP实现原理是由hash数组为主，存储一个key-val结构entry类的数组，当出现hash冲突时,通过链表来    解决问题。Jdk1.8中引入了红黑树,当链表的长度大于8 时会自动将链表转成红黑树。

   hashMAp线程不安全，hashtable线程安全。Hash Table时不支持null的，hashmap支持nulll是因为将null放入hash表的0个buchect。

   实现线程安全的两种方式：Collecttions.synchronizedMap()也可以用ConcurrentHashMap。Jdk7时通过桶的分段锁的方式实现，默认设置16段，当并发度超过16段    时按2的指幂增长。JDK8放弃分段锁的实现，通过节点的原子锁来实现锁。将分段锁的悲观锁改成平台型的乐观锁。乐观锁无法保证脏读，所以要通过原子快照来保证。
   
   [concurrenthashmap 线程安全原理] (http://www.importnew.com/22007.html)
   
 *  __使用HashMap有什么性能问题吗?__
 
   当大量的key出现hash冲突时，链表会变长，从而影响get、put效率。而且当链表长度达到负载因子设置0.75长度值时，还会有扩容操作会很影响性能。
   
*  __hashMap默认大小是多少?内部是怎么扩容的?__

   hashMap这里的默认值是16。当元素个数大于0.75×16 = 12时，HashMap会自动进行扩容。 oldlength *2个
   
*  __怎么按添加顺序存储元素?怎么按A-Z自然顺序存储元素?怎么自定义排序?__

   1､hashMap的存储是无序的，想要有序存储需要在存储的key有序。其根本原因是存储位置是由hashcode决定的，hashcode是由key计算得来的。

   2､通过Collections.sort()来排序。
   
* __HashMap使用对象作为key，如果hashcode相同会怎么处理?__

   在hashmap中，由于key是不可以重复的，他在判断key是不是重复的时候就判断了hashcode这个方法，而且也用到了equals方法。这里不可以重复是说equals和          hashcode只要有一个不等就可以了。
   
*  __HashMap中的get操作是什么原理?__

   只需要根据key的hashcode算出元素在数组中的下标,之后遍历Entry对象链表,直到找到元素为止。
   
* __TCP和UDP的区别，TCP为什么是三次握手，不是两次？__

     **** TCP与UDP基本区别:

     1､基于连接与无连接

     2､TCP要求系统资源较多，UDP较少;

     3､UDP程序结构较简单

     4､流模式(TCP)与数据报模式(UDP);

     5､TCP保证数据正确性，UDP可能丢包

     6､TCP保证数据顺序，UDP不保证
     
     ****三次握手过程:

     第一次握手：建立连接时,客户端发送syn包(syn=j)到服务器,并进入SYNSEND ,等待服务器确认。

     第二次握手：服务器收到syn包，必须确认客户端的SYN （ ack=j+1 ），同时自己也发送一个SYN包（syn=k）即SYN+ACK包 ,此时服务器进入 SYNRECV状态;

     第三次握手：客户端收到服务器的SYN+ACK包,向服务器发送确认包ACK(ack=k+1),此包发送完毕,客户端和服务器进入ESTABLISHED状态,完成三次握手
     
 *  __switch中可以使用String吗?__
 
    在jdk 7 之前，switch 只能支持 byte、short、char、int 这几个基本数据类型和其对应的封装类型。Java 7中加入了对String类型的支持,底层编译时将语句转换     成if-else语句，支持String只是为了简化书写。不建议在switch中使用String。
    
 *  __String、StringBuffer、StringBuilder有什么区别?__
 
    1､首先说运行速度，或者说是执行速度，在这方面运行速度快慢为:StringBuilder > StringBuffer > String

    2､在线程安全上，StringBuilder是线程不安全的，而StringBuffer是线程安全的

    3､应用场景，String-适用于少量的字符串操作的情况;StringBuilder-适用于单线程下在字符缓冲区进行大量操作的情况;StringBuffer-适用多线程下在字符缓冲区       进行大量操作的情况。
    
*  __可以自定义java.lang.String类并使用吗?__

   #### 不能！
   
   Java类加载机制为代理模式，先交给其父加载器去加载，如果父加载器加载不了，则由自己加载。

   我们自定义的类是由系统类加载器进行加载，而它的父加载器为扩展类加载器，扩展类加载器为引导类加载器。我们定义的java.lang.String最先由引导加载器加载，    而它负责加载Java核心库，但java.lang.String正是系统中的类，已经被引导加载器记载过了，所以不再加载自定义的java.lang.String。
   
* __finally块一定会执行吗?__

  #### 不一定！

   1､finally没在作用域无法执行。

   2､主线程退出也无法执行。
   
*  __线程和进程的区别是什么?__

      1､进程是具有一定独立功能的程序关于某个数据集合上的一次运行活动,进程是系统进行资源分配和调度的一个独立单位。

      2､线程是进程的一个实体, 是CPU调度和分派的基本单位,它是比进程更小的能独立运行的基本单位.线程自己基本上不拥有系统资源,只拥有一点在运行中必不可少的         资源(如程序计数器,一组寄存器和栈),但是它可与同属一个进程的其他的线程共享进程所拥有的全部资源。

      3､一个线程可以创建和撤销另一个线程，同一个进程中的多个线程之间可以并发执行。
      
*  __Java实现线程有哪几种方式?__

      1、继承Thread类实现多线程

      2、实现Runnable接口方式实现多线程

      3、使用ExecutorService、Callable、Future实现有返回结果的多线程
      
*  __一个线程的生命周期有哪几种状态?它们之间如何流转的?__

      1、新建状态(New):新创建了一个线程对象。

      2、就绪状态(Runnable)：线程对象创建后，其他线程调用了该对象的start()方法。该状态的线程位于“可运行线程池”中，变得可运行，只等待获取CPU的使用权。          即在就绪状态的进程除CPU之外，其它的运行所需资源都已全部获得。

      3、运行状态(Running)：就绪状态的线程获取了CPU，执行程序代码。4、阻塞状态(Blocked):阻塞状态是线程因为某种原因放弃CPU使用权，暂时停止运行。直到线          程进入就绪状态，才有机会转到运行状态。
      
     #### 阻塞的情况分三种:

      (1)、等待阻塞:运行的线程执行wait()方法，该线程会释放占用的所有资源，JVM会把该线程放入“等待池”中。进入这个状态后，是不能自动唤醒的，必须依靠其他            线程调用notify()或notifyAll()方法才能被唤醒，

      (2)、同步阻塞:运行的线程在获取对象的同步锁时，若该同步锁被别的线程占用，则JVM会把该线程放入“锁池”中。

      (3)、其他阻塞:运行的线程执行sleep()或join()方法，或者发出了I/O请求时，JVM会把该线程置为阻塞状态。当sleep()状态超时、join()等待线程终止或者超              时、或者I/O处理完毕时，线程重新转入就绪状态。

      5、死亡状态(Dead):线程执行完了或者因异常退出了run()方法，该线程结束生命周期。
      
*  __多线程同步有哪几种方法?  __   

      1､同步方法,即有synchronized关键字修饰的方法。

      2.同步代码块,即有synchronized关键字修饰的语句块。

      3､使用特殊域变量(volatile)实现线程同步:

      a).volatile关键字为域变量的访问提供了一种免锁机制，

      b).使用volatile修饰域相当于告诉虚拟机该域可能会被其他线程更新，

      c).因此每次使用该域就要重新计算，而不是使用寄存器中的值d.volatile不会提供任何原子操作，它也不能用来修饰final类型的变量
      

      4､使用重入锁实现线程同步,在JavaSE5.0中新增了一个java.util.concurrent包来支持同步。

      5､使用局部变量实现线程同步 ,如果使用ThreadLocal管理变量，则每一个使用该变量的线程都获得该变量的副本，副本之间相互独立，这样每一个线程都可以随意         修改自己的变量副本，而不会对其他线程产生影响。
      
* __什么是死锁?如何避免死锁?__

     #### 产生死锁的原因主要是:

     (1) 因为系统资源不足。

     (2) 进程运行推进的顺序不合适。

     (3) 资源分配不当等。

     #### 产生死锁的四个必要条件:

     (1) 互斥条件:一个资源每次只能被一个进程使用。

     (2) 请求与保持条件:一个进程因请求资源而阻塞时，对已获得的资源保持不放。

     (3) 不剥夺条件:进程已获得的资源，在末使用完之前，不能强行剥夺。

     (4) 循环等待条件:若干进程之间形成一种头尾相接的循环等待资源关系。
     
 *  __多线程之间如何进行通信?__
 
       1､同步，这里讲的同步是指多个线程通过synchronized关键字这种方式来实现线程间的通信。

      2､while轮询的方式。

      3､wait/notify机制。

      4､管道通信就是使用java.io.PipedInputStream 和java.io.PipedOutputStream进行通信
      
* __新建T1、T2、T3三个线程，如何保证它们按顺序执行?__

     T3先执行，在T3的run中，调用t2.join，让t2执行完成后再执行t3 在T2的run中，调用t1.join，让t1执行完成后再让T2执行
     
* __为什么要使用线程池?__

     #### 线程的执行过程: 
     创建(t1) 运行(t2) 销毁(t3) 线程运行的总时间 T= t1+t2+t3; 
     假如，有些业务逻辑需要频繁的使用线程执行某些简单的任务，那么很多时间都会浪费t1和t3上。为了避免这种问题，JAVA提供了线程池 在线程池中的线程可以复        用，当线程运行完任务之后，不被销毁.
     
* __常用的几种线程池并讲讲其中的工作原理。__

     1、newCachedThreadPool,创建一个可缓存线程池，如果线程池长度超过处理需要，可灵活回收空闲线程，若无可回收，则新建线程。

        线程池特点:

        工作线程的创建数量几乎没有限制(其实也有限制的,数目为Interger. MAX_VALUE), 这样可灵活的往线程池中添加线程。

        如果长时间没有往线程池中提交任务，即如果工作线程空闲了指定的时间(默认为1分钟)，则该工作线程将自动终止。终止后，如果你又提交了新的任务，则线程池         重新创建一个工作线程。在使用CachedThreadPool时，一定要注意控制任务的数量，否则，由于大量线程同时运行，很有会造成系统瘫痪。

     2、newFixedThreadPool，定长线程。创建一个指定工作线程数量的线程池。每当提交一个任务就创建一个工作线程，如果工作线程数量达到线程池初始的最大数，则         将提交的任务存入到池队列中。FixedThreadPool是一个典型且优秀的线程池，它具有线程池提高程序效率和节省创建线程时所耗的开销的优点。但是，在线程池         空闲时，即线程池中没有可运行任务时，它不会释放工作线程，还会占用一定的系统资源。

     3.newScheduledThreadPool,定长、周期性线程池

     4、newSingleThreadExecutor,单线程。创建一个单线程化的Executor，即只创建唯一的工作者线程来执行任务，它只会用唯一的工作线程来执行任务，保证所有任         务按照指定顺序(FIFO, LIFO, 优先级)执行。如果这个线程异常结束，会有另一个取代它，保证顺序执行。单工作线程最大的特点是可保证顺序地执行各个任务，         并且在任意给定的时间不会有多个线程是活动的。
     
* __什么是守护线程?有什么用?__

     1､守护线程就是main同生共死，当main退出，它将终止，而普通线程是在任务执行结束才停止。2.Java虚拟机在它所有非守护线程已经离开后自动离开。守护线程则        是用来服务用户线程的，如果没有其他用户线程在运行，那么就没有可服务对象，也就没有理由继续下去。守护线程是用来保证用户线程，有效可靠的执行。
     
 * __Java中notify和notifyAll有什么区别?__
 
     notify是通知一个线程获取锁，notifyAll是通知所有相关的线程去竞争锁。notify不能保证获得锁的线程，真正需要锁，并且可能产生死锁。
     
* __提交任务时线程池队列已满会时发会生什么?__

    如果一个任务不能被调度执行那么ThreadPoolExecutor’s submit()方法将会抛出一个RejectedExecutionException异常。
    
*  __ThreadLocal实现原理是什么?__

     ThreadLocal整体上感觉是，一个包装类。声明了这个类的对象之后，每个线程的数据其实还是在自己线程内部通过threadLocals引用到的自己的数据。只是通过        ThreadLocal访问这个数据而已。当线程中的threadlocalmap是null的时候，会调用createmap创建一个map。同时根据函数参数设置上初始值。也就是说，当前        线程的threadlocalmap是在第一次调用set的时候创建map并且设置上相应的值的。
     
     # Java-Web
     
