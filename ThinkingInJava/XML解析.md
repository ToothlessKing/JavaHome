
## 一、java 解析xml常见的四种方式
### 1、Dom 解析

&emsp;Dom（文档对象模型），DOM是针对HTML文档、XML等文档的一套API，用来访问或操作HTML文档、XHTML文档、XML文档中的节点元素。
解析器读入整个文档，然后构建一个驻留内存的树结构DOM接口来操作这个树结构。  
&emsp;优点：整个文档树在内存中，便于操作；支持删除、修改、重新排列等多种功能;  
&emsp;缺点：将整个文档调入内存（包括无用的节点），浪费时间和空间，所以dom不适合于包含大量数据的xml解析;  
&emsp;使用场合：一旦解析了文档还需多次访问这些数据；硬件资源充足（内存、CPU）。  
&emsp;详情请参见：[Dom及Dom解析实例](http://blog.csdn.net/zp357252539/article/details/48084509)
### 2、SAX解析
&emsp;它不同于DOM的文档驱动，它是事件驱动的，它并不需要读入整个文档，而文档的读入过程也就是SAX的解析过程。所谓事件驱动，
是指一种基于回调（callback）机制的程序运行方法。      &emsp;优点：只在读取数据时检查数据，不需要保存在内存中；可以在某个条件得到满足时停止解析，不必解析整个文档；效率和性能较高，能解析大于系统内存的文档。     
&emsp;缺点：无法定位文档层次，很难同时访问同一文档的不同部分数据，不支持XPath。  
&emsp;详情请参见[Sax解析XML](http://blog.csdn.net/wangkuifeng0118/article/details/7305068)  
### 3、JDom  
&emsp;DOM的目的是成为Java特定文档模型，它简化与XML的交互并且比使用DOM实现更快，DOM与DOM主要有两方面不同。首先，JDOM仅使用具体类而不使用接口。这在某些方面简化了API，但是也限制了灵活性。第二，API大量使用了Collections类，简化了那些已经熟悉这些类的Java开发者的使用
  http://blog.csdn.net/qh_java/article/details/50499973
  http://blog.chinaunix.net/uid-354915-id-3877243.html
### 4、Dom4J
&emsp;它合并了许多超出基本XML文档表示的功能，包括集成的XPath支持、XML Schema支持以及用于大文档或流化文档的基于事件的处理。
它还提供了构建文档表示的选项，它通过DOM4J API和标准DOM接口具有并行访问功能。   
&emsp;大量使用了Java集合类，方便Java开发人员，同时提供一些提高性能的替代方法。
&emsp;支持XPath。
&emsp;有很好的性能。
&emsp;大量使用了接口，API较为复杂。  
详情请参见[java使用dom4j解析XMl](http://blog.csdn.net/yyywyr/article/details/38359049)

## 二、XPath  
xpath就是选择XML文件中节点的方法  
- element（元素节点） 
- attribute（属性节点） 
- text （文本节点）  
- namespace （名称空间节点）  
- processing-instruction （处理命令节点）  
- comment （注释节点）  
- root （根节点）  
xpath通过"路径表达式"（Path Expression）来选择节点。可以是绝对路径（“/”起首，后面跟着根节点），也可以时相对路径，基本规则如下：
- nodename（节点名称）：表示选择该节点的所有子节点
- "/"：表示选择根节点
- "//"：表示选择任意位置的某个节点
- "@"： 表示选择某个属性
  例子：
  ’
  <bookstore>
    <book>
      <title lang="eng">Harry Potter</title>
      <price>29.99</price>
    </book>
    <book>
      <title lang="eng">Learning XML</title>
      <price>39.95</price>
    </book>
  </bookstore>
‘
  http://www.cnblogs.com/fdszlzl/archive/2009/06/02/1494836.html
  http://www.cnblogs.com/zhangfei/p/4283930.html   

## 三、Json与xml比较
  
## 四、demo：简单还原Spring iop 的功能
