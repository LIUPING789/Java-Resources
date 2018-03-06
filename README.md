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
