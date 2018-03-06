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
