
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
 
### 4、Dom4J
&emsp;它合并了许多超出基本XML文档表示的功能，包括集成的XPath支持、XML Schema支持以及用于大文档或流化文档的基于事件的处理。
它还提供了构建文档表示的选项，它通过DOM4J API和标准DOM接口具有并行访问功能。   
&emsp;大量使用了Java集合类，方便Java开发人员，同时提供一些提高性能的替代方法。
&emsp;支持XPath。
&emsp;有很好的性能。
&emsp;大量使用了接口，API较为复杂。  
详情请参见[java使用dom4j解析XMl](http://blog.csdn.net/yyywyr/article/details/38359049)、
  [四种解析优缺点](http://blog.csdn.net/qh_java/article/details/50499973)、
  [四种解析比较](http://blog.chinaunix.net/uid-354915-id-3877243.html)
## 二、XPath  
xpath就是选择XML文件中节点的方法  
> - element（元素节点） 
> - attribute（属性节点） 
> - text （文本节点）  
> - namespace （名称空间节点）  
> - processing-instruction （处理命令节点）  
> - comment （注释节点）  
> - root （根节点）  
xpath通过"路径表达式"（Path Expression）来选择节点。可以是绝对路径（“/”起首，后面跟着根节点），也可以时相对路径，基本规则如下：
> - nodename（节点名称）：表示选择该节点的所有子节点
> - "/"：表示选择根节点
> - "//"：表示选择任意位置的某个节点
> - "@"： 表示选择某个属性
  例子：

```XML
<bookstore>
  <book>
     <title lang="eng">Harry Potter</title>
     <price>29.99</price>
  </book>
  <book> 
     <title lang="eng">Learning XML</title>
     <price>39.95</price>
     </book>
  </bookstore >
 ``` 
 
> /bookstore ：选取根节点bookstore，这是绝对路径写法。  
> bookstore/book ：选取所有属于 bookstore 的子元素的 book元素，这是相对路径写法。   
> //book ：选择所有 book 子元素，而不管它们在文档中的位置。  
> bookstore//book ：选择所有属于 bookstore 元素的后代的 book 元素，而不管它们位于 bookstore 之下的什么位置。  
> /bookstore/book[1] ：表示选择bookstore的第一个book子元素。  
> //title[@lang='eng'] ：表示选择所有lang属性的值等于"eng"的title节点  

详情请参见[Xpath路径表达式](http://www.ruanyifeng.com/blog/2009/07/xpath_path_expressions.html)、[java结合XPATH解析XML](http://www.cnblogs.com/zhangfei/p/4283930.html)、[Xpath 详解](http://www.cnblogs.com/fdszlzl/archive/2009/06/02/1494836.html)  
   

## 三、Json与xml比较
  [Xml与json比较](http://www.cnblogs.com/SanMaoSpace/p/3139186.html)
## 四、demo:解析book.xml
book.xml 如下：

```XML
    <书架 id =“root”>  
      <书 id = "book1">  
        <书名 id="1">think in java</书名>  
        <作者 id="author">李狗蛋</作者>  
        <售价>89</售价>  
      </书>
      <书 >  
        <书名 id="2">java core</书名>  
        <作者 >李狗蛋</作者>  
        <售价>78</售价>  
      </书>  
    </书架>
```

### Sax解析
[DefaultHandler方法](http://blog.csdn.net/sir_zeng/article/details/17710013)

```java
  public class SAXParse  implements ParseXml{ //ParseXml是自己定义的接口 
    private List<Book> list;  
    private BeanListHandler handler;   
    public SAXParse(String filePath) throws Exception{  
      SAXParserFactory factory = SAXParserFactory.newInstance();//创建解析工厂     
      SAXParser parser = factory.newSAXParser();//创建解析器
      XMLReader reader = parser.getXMLReader(); //得到读取器  
      handler = new BeanListHandler();//实例化DefaultHandler对象 
      reader.setContentHandler(handler);//设置处理
      reader.parse(filePath); 
    }
    public List<Book> getBooks(){
      list = handler.getBooks();
      return list;
    }
 }   
 public class BeanListHandler extends DefaultHandler{
   ArrayList<Book> list = new ArrayList<Book>();
   private String currentTag;
   private Book book;
   
  @Override 
  public void startElement (String uri,String localname,String qname ,Attributes attributes) throws SAXException{
  
   currentTag = qName;
   if("书".equalsIgnoreCase(currentTag)){
     book = new Book();
   }
  }
  @Override 
  public void characters(char ch[],int start,int length) throws SAXException{
   
   if("书名".equals(currentTag)){
     String  name = new String(ch,start,length);
     book.setName(name);
   }
   if("作者".equals(currentTag)){
     String author = new String(ch.start,length);
     book.setAuthor(author);
   }
   if("售价".equals(currentTag)){
     String price = new String(ch,start,length);
     book.setPrice(price);
   }
  }
  
  @Override
  public void endElement(String uri,String localName,String qName) throws SAXException{
   if("书".equals(qName)){
     list.add(book);
     book = null;
   }
   currentTag = null;
  }
  
  public ArrayList<Book> getBooks(){
   return list;
  }
 }
```

### Jdom解析
需要jdom.jar

```java
  public class Jdom implements ParseXML{
    private Element root;
    List<Book> list = new ArrsyList<Book>();
    public Jdom(String filePath) throws Exception {
      SAXBuilder builder = new SAXBuilder();//创建解析器
      InputStream file = new FileInputStream(filePath);//创建输入流
      Document doc = builder.build(file);//获取Document对象，以后的操作都是对Document对象进行操作的
      root = doc.getRootElement();//得到根节点
    }
    public List<Book> getBooks(){
      List<Element> list1 = root.getChildren("书");//获取节点名称为“书”的节点集合
      Book book;
      for(Element e:list1){//遍历节点
        book = new Book();
        book.setName(e.getChildText("书名"));
        book.setAuthor(e.getChildText("作者"));
        book.setPrice(e.getChildTest("售价"));
        list.add(book);
      }
      return list;
    }
  }
```

### Dom4j解析
需要dom4j.jar

```java
  public class Dom4J implements ParseXML{
  
    private Element rootElmt;
    List<Book> list = new ArrayList<Book>()
    Book book;
    
    public Dom4J(String filePath) throws Exception{
      File file = new File(filePath);
      SAXReader reader = new SAXReader();//创建SAXReader对象
      Document doc = reader.read(file); //读取文件 转换成Document  
      rootElmt = doc.getRootElement();//获取根节点元素对象
    }
    public List<Book> getBooks(Element node){
      if(node.getName().equals("书")){
        book = null;
        book = new Book();
      }
      if(node.getName().equals("书名")){
        book.setName(node.getText());
      }
      if(node.getName().equals("作者")){
        book.setAuthor(node.getText());
      }
      if(node.getName().equals("售价")){
        book.setPrice(node.getText());
        lost.add(book);
      }
      Iterator<Element> iterator = node.elementIterator();
      while(iterator.hasNext()){
        Element node2 = iterator.next();
        getBooks(node2);
      }
      return list;
    }
    public List<Book> getBooks(){
     return getBooks(rootElmt); 
    }
  }
```

### 测试类

```java
  public static void main(String[] args) {
    ParsrXml parseXml = new Dom4J("src/main/book.xml");
    List<Book> list = parseXml.getBooks();
    Book book;
    for(int i=0 ; i<list.size() ;i++){
      book = new Book();
      book = (Book)list.get(i);
      System.out.println(book);
    }
  }
```

### XPath  应用(需要)
需要jaxen.jar、dom4j.jar，因为dom4j支持Xpath，所以使用dom4j进行解析

```java
  public class XPath{
    private String filePath;
    private Document documentl
    
    public XPath(String filePath){
      this.filePath =filePath;
      this.load(filePath);
    }
    private void load(String filePath){
      File file = new File(filePath);
      if(file.exists()){
        SAXReader saxReader = new SAXReader();//创建SAXReader对象
        try {
          document = saxReader.read(file);//读取文件 转换成Document 
        }catch(Exception e){
          e.printStackTrace();
        }
      }
    }
    public List<Element> getElementObject(String elementPath){
      return document.selectNodes(elementPath);
    }
    public String getValues(){
      List<Elements> elements = getElementObject(elementPath);
      String name ="";
      for(Element element : elements){
        name = element.getName() + " : " +element.getText()+"\n";
      }
      return name ;
    }
    public static void main(String[] args){
      XPath xPath = new XPath("src/main/book.xml");
      String value = xPath.getValues("//书[售价>80]/书名");
      String value2 = xPath.getValues("书架/书/售价[.>80]");
      String value3 = xPath.getValues("书架/书/*[@id=’2‘]")；
    }
  }
```
