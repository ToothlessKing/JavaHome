
## 一、java 解析xml常见的四种方式
### 1、Dom 解析

　　Dom（文档对象模型），DOM是针对HTML文档、XML等文档的一套API，用来访问或操作HTML文档、XHTML文档、XML文档中的节点元素。
解析器读入整个文档，然后构建一个驻留内存的树结构， 然后代码就可以使用 DOM 接口来操作这个树结构。

　　优点：整个文档树在内存中，便于操作；支持删除、修改、重新排列等多种功能；
　　
　　缺点：将整个文档调入内存（包括无用的节点），浪费时间和空间，所以dom不适合于包含大量数据的xml解析；
　　
&emsp;使用场合：一旦解析了文档还需多次访问这些数据；硬件资源充足（内存、CPU）。
　　
详情请参见：[Dom及Dom解析实例](http://blog.csdn.net/zp357252539/article/details/48084509)
### 2、SAX解析
  它不同于DOM的文档驱动，它是事件驱动的，它并不需要读入整个文档，而文档的读入过程也就是SAX的解析过程。所谓事件驱动，
是指一种基于回调（callback）机制的程序运行方法。
  优点：只在读取数据时检查数据，不需要保存在内存中；可以在某个条件得到满足时停止解析，不必解析整个文档；效率和性能较高，能解析大于系统内存的文档。
  缺点：无法定位文档层次，很难同时访问同一文档的不同部分数据，不支持XPath。
  http://blog.csdn.net/wangkuifeng0118/article/details/7305068
### 3、Dom4J
  它合并了许多超出基本XML文档表示的功能，包括集成的XPath支持、XML Schema支持以及用于大文档或流化文档的基于事件的处理。
它还提供了构建文档表示的选项，它通过DOM4J API和标准DOM接口具有并行访问功能
  大量使用了Java集合类，方便Java开发人员，同时提供一些提高性能的替代方法。
  支持XPath。
  有很好的性能。
  大量使用了接口，API较为复杂。
###\4、JDom
  http://blog.csdn.net/qh_java/article/details/50499973
  http://blog.chinaunix.net/uid-354915-id-3877243.html
## 二、XPath
  http://www.cnblogs.com/fdszlzl/archive/2009/06/02/1494836.html
  http://www.cnblogs.com/zhangfei/p/4283930.html
## 三、Json与xml比较
  
## 四、demo：简单还原Spring iop 的功能
