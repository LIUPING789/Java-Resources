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
