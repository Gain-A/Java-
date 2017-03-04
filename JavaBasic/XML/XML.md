# XML #
* 什么是XML？
 * 可拓展标记语言--Extensible Markup Language
* 为什么学习XML
 * HTML的局限性（拓展性、结构性、移植性、数据交换...）
 * XML可以弥补HTML的缺陷
## 格式正确的XML文件规则（Well-Formed XML） ##
1. XML声明必须以小写xml声明，在首行设置version属性
2. 一份文件中必须有唯一、单一的根元素
3. 所有的标记必须以嵌套式排列（树状，不得交叉）
4. 每一个元素都必须有一个开始和结束标签（除了空标签）
5. 标签名称与属性必须合法，**大小写视为不同**
6. 属性值必须以引号（“或‘）包含
7. 特殊字符按规定编写
### XML语法 ###
* XML宣告
 * <?xml version="1.0" encoding="GB2312"?>
 * 该宣告会为XML解析器定义该文件为XML文件
* 元素(elements)与属性(attributes)
#### 标签名称和属性的规定 ####
* 第一个字符必须为英文字符或其它文字，如生命为GB2312时可以用中文_或：
* 其它字符（除第一个外）必须为应为字母或其它文字，如声明GB2312时，可以用"中文"或"_"、:、"一"、"数字"
* 注意<:author>在IE5.0中被定义为不合法
#### 特殊字符的规定 ####
* 在XML文件中，有些字符用来做特殊用途，如"<",">"做标记符，" " ","'"属性的设置符，"&"实体的引用符号

|写法|代表符号|
|::|::|
|`&lt;`|<|
|`&gt;`|>|
|`&amp;`|&|
|`&apos;`|'|
|`&quot;`|"|

# XML解析器概述 #
* XMl解析器
 在读取XML文档并将文档分解为可进行分析的几个元素的过程
* 处理XML文档
 * 解析检查XML文档的有效性和格式规范
 * 创建解析树并将其传递给呈现代理程序
 * 呈现代理程序将显示此解析树
 *  解析器将创建一系列对象，用于显示域XML文档关联的样式表
## XML解析器 ##
* DOM
* SAX
* JDOM
* DOM4J
### 文档对象模型DOM ###
DOM(Document Object Model)
* W3C指定的一套跨平台和语言标准，表示文档内容和模型
* 用Level（级别）的形式代替版本。
 * Level1定义了文档中内容的功能和查找功能
 * Level2提供了对XML，HTML和CSS等内容模型的模块和选项
 * Level3指定中，为特定类型提供更多的工具如XML的验证公交等
* 基于对象的将XML文档表示为树
* 在内存中解析和存储XML文档
* 允许随机访问文档的不同部分
* DOM解析把XML文档转化为一个包含内容的树，并可以对树进行遍历
* 树模型
 * 每个项目都表示一个节点
 * 每个终端项目都表示一个叶节点
 * 直接上级节点表示父节点
 * 任何上级节点都表示祖先节点
 * 从树的一个部分可以到达数的任何其他部分
#### 使用DOM解析XML文档 ####
	/**
	 * 从指定文件中，解析数据库配置信息
	 * @param file
	 * @return 包含配置信息url,username,password的键值对
	 */
	public static HashMap<String, String> parseConfig(File file){
		HashMap<String, String> map = null;
		//解析config.xml获得数据库名、用户名、密码
		try {
			//1. 新建Document对象
			Document docu = DocumentBuilderFactory.newInstance().newDocumentBuilder().parse(file);
			//2. 得到connection节点
			Element conn = (Element) docu.getElementsByTagName("connection").item(0);
			//3. 得到connection的子节点并给Map赋值
			NodeList list = conn.getChildNodes();
			map = new HashMap<>();
			map.put("url", list.item(0).getTextContent());
			map.put("username", list.item(1).getTextContent());
			map.put("password", list.item(2).getTextContent());
			
		} catch (ParserConfigurationException e) {
			e.printStackTrace();
		} catch (SAXException e) {
			e.printStackTrace();
		} catch (IOException e) {
			e.printStackTrace();
		}
		return map;
	}
#### 使用DOM生成XML文档 ####
	/**
	 * 向指定目录下生成默认配置文件
	 * @param file 要保存到的文件
	 * @param dbName 数据库名称
	 * @param username 用户名
	 * @param password 密码
	 */
	public static void createConfig(File file, String dbName, String username, String password){
		try {
			//1. 获得Document对象
			Document docu = DocumentBuilderFactory.newInstance().newDocumentBuilder().newDocument();
			//2. 创建节点
			Element root = docu.createElement("jdbc");
			Element conn = docu.createElement("connection");
			Element db = docu.createElement("url");
			Element urName = docu.createElement("username");
			Element psd = docu.createElement("password");
			//3. 为节点赋值
			db.setTextContent("jdbc:mysql://localhost:3306/" + dbName + "?characterEncoding=utf8");
			urName.setTextContent(username);
			psd.setTextContent(password);
			//4. 设置节点之间的关系
			root.appendChild(conn);
			conn.appendChild(db);
			conn.appendChild(urName);
			conn.appendChild(psd);
			docu.appendChild(root);
			
			//5. 输出文件
			TransformerFactory tf = TransformerFactory.newInstance();
			Transformer trans = tf.newTransformer();
			DOMSource source = new DOMSource(docu);
			StreamResult result = new StreamResult(file);
			trans.transform(source, result);
			
		} catch (ParserConfigurationException e) {
			e.printStackTrace();
		} catch (TransformerConfigurationException e) {
			e.printStackTrace();
		} catch (TransformerException e) {
			e.printStackTrace();
		}
	}
#### DOM的使用场景和缺点 ####
* DOM最适用的场景
 * 在结构上修改XML文档时
 * 在内存中与其它应用程序共享文档时
* DOM的缺点
 * 将整个文档存储在内存中
 * 方法命名管理不符合Java编程管理
### SAX(Simple API for XML) ###
基于事件驱动，使用回调机制将重要事件通知给客户端应用程序

* 简单SAX应用程序的组件包括：
 * 应用程序
 	 * 创建一个解析器和文档处理工具
 	 * 告诉解析器使用哪个文档处理程序
 	 * 告诉解析器处理文档 
 * 解析器
	 * 将重要事件通知给文档处理程序
 * 文档处理程序 
 	 * 处理通知
#### 用于XML解析的Java API ####
* 可使用SAX的普通API
* 作为javax.xml包实现
* 易于安装且快速
* 更具一致性
* 使用factory设计模式创建要解析的对象
#### SAXParserHandler类 ####
* 解释如何捕获和响应各个事件
* startDocument()和endDocument()事件是在文档的起始处和结束处被激发的
* startElement()和endElement()是在遇到起始标记和结束标记时被激发的
* characters()事件是在遇到字符数据时被激发的
#### 使用SAX解析XML文档的步骤如下 ####
* 创建SAXParserFactory实例
* 创建SAXParser实例
* 创建SAXParserHandler类
* 使用parse()方法解析XML文档

		/**
		 * 解析xml文件
		 * @return ArrayList<>
		 */
		public ArrayList<Book> parseXML() {
			//获取一个SAXParserFactory的实例
			SAXParserFactory factory = SAXParserFactory.newInstance();
			ArrayList<Book> bookList = null;
			//通过factory 获取SAXParser实例
			try {
				SAXParser parser = factory.newSAXParser();
				SAXHandler handler = new SAXHandler();
				parser.parse("books.xml", handler);
				bookList = handler.getBookList();
				int size = bookList.size();
				System.out.println("共有"+size+"本书");	
				for(Book book : bookList) {
					System.out.println(book.getId());
					System.out.println(book.getName());
					System.out.println(book.getAuthor());
					System.out.println(book.getPrice());
					System.out.println(book.getYear());
					System.out.println(book.getLanguage());
					System.out.println("-----------------finish");
				}
			} catch (ParserConfigurationException e) {
				e.printStackTrace();
			} catch (SAXException e) {
				e.printStackTrace();
			} catch (IOException e) {
				e.printStackTrace();
			}
			return bookList;
		}

		/**
		 * 生成xml文件
		 */
		public void createXml() {
			ArrayList<Book> bookList = parseXML();
			//创建一个TrasformerFactory类的对象 
			SAXTransformerFactory stff = (SAXTransformerFactory) SAXTransformerFactory.newInstance();
			try {
				//通过SAXTransformerFactory对象创建TransformerHandler对象
				TransformerHandler tfh = stff.newTransformerHandler();
				Transformer tf = tfh.getTransformer();
				//通过Transformer对象对生成的xml文件进行设置
				//设置xml的编码
				tf.setOutputProperty(OutputKeys.ENCODING, "UTF-8");
				//设置xml是否换行
				tf.setOutputProperty(OutputKeys.INDENT, "yes");
				//创建一个Result对象
				File file = new File("books1.xml");
				if (!(file.exists())) {
					file.createNewFile();
				}
				//创建result对象并且使其与handler关联
				Result res = new StreamResult(new FileOutputStream(file));
				tfh.setResult(res);
				//利用handler对象进行xml文件内容的编写
				tfh.startDocument();
				AttributesImpl attr = new AttributesImpl();
				tfh.startElement("", "", "bookstore", attr);
				for(Book book : bookList) {
					attr.clear();
					attr.addAttribute("", "", "id", "", book.getId());
					tfh.startElement("", "", "book", attr);
					//创建name节点
					if ((book.getName() != null) && !(book.getName().trim().equals(""))) {
						attr.clear();
						tfh.startElement("", "", "name", attr);
						tfh.characters(book.getName().toCharArray(), 0, book.getName().length());
						tfh.endElement("", "", "name");
					}
					//创建author节点
					if ((book.getAuthor() != null) && !(book.getAuthor().trim().equals(""))) {
						attr.clear();
						tfh.startElement("", "", "author", attr);
						tfh.characters(book.getAuthor().toCharArray(), 0, book.getAuthor().length());
						tfh.endElement("", "", "author");
					}
					//创建year节点
					if ((book.getYear() != null) && !(book.getYear().trim().equals(""))) {
						attr.clear();
						tfh.startElement("", "", "year", attr);
						tfh.characters(book.getYear().toCharArray(), 0, book.getYear().length());
						tfh.endElement("", "", "year");
					}
					//创建price节点
					if ((book.getPrice() != null) && !(book.getPrice().trim().equals(""))) {
						attr.clear();
						tfh.startElement("", "", "price", attr);
						tfh.characters(book.getPrice().toCharArray(), 0, book.getPrice().length());
						tfh.endElement("", "", "price");
					}
					//创建language节点
					if ((book.getLanguage() != null) && !(book.getLanguage().trim().equals(""))) {
						attr.clear();
						tfh.startElement("", "", "language", attr);
						tfh.characters(book.getLanguage().toCharArray(), 0, book.getLanguage().length());
						tfh.endElement("", "", "language");
					}
					tfh.endElement("", "", "book");
				}
				tfh.endElement("", "", "bookstore");
				tfh.endDocument();
				
			} catch (TransformerConfigurationException e) {
				e.printStackTrace();
			} catch (FileNotFoundException e) {
				e.printStackTrace();
			} catch (IOException e) {
				e.printStackTrace();
			} catch (SAXException e) {
				// TODO Auto-generated catch block
				e.printStackTrace();
			}
			
		}


#### SAX使用场景和缺点 ####
* SAX最适用的场景
 * 需要在解析大型文件时
 * 在只需一个信息子集时
* SAX的缺点
 * 不能对文档进行随机访问  
 * 只读
 * 只遍历文档一次
### JDOM ###
jdom包的结构包括：

* org.jdom  包含了所有的xml文档要素的Java类
* org.jdom.adapters    包含了与dom适配的Java类
* org.jdom.filter包含了xml文档的过滤器类
* org.jdom.input包含了读取xml文档的类
* org.jdom.output包含了写出xml文档的类
* org.jdom.transform包含了将jdom xml文档接口转换为其它xml文档接口
* org.jdom.xpath包含了对xml文档xpath操作的类
#### JDOM解析 ####
	/**
	 * 解析xml文件
	 */
	public void parseXML() {
		//进行对books.xml文件的jdom解析
		SAXBuilder saxBuilder = new SAXBuilder();
		FileInputStream in;
		try {
			//创建一个输入流，将xml文件加载到输入流中
			in = new FileInputStream("src/res/books.xml");
			//通过saxBuilder将输入流加载到saxBuilder中
			Document docu = saxBuilder.build(in);
			//通过document对象获取xml文件的根节点
			Element rootElement = docu.getRootElement();
			//获取根节点下子节点的集合
			 List<Element> bookList = rootElement.getChildren();
			 //继续进行解析
			 for (Element book : bookList) {
				 Book bookEntity = new Book();
				 System.out.println("---------------开始解析第"+(bookList.indexOf(book) + 1)+"本书-----------");
				 //解析book的属性
				 List<Attribute> attrList = book.getAttributes();
				 //遍历attrList
				 for (Attribute attr : attrList) {
					 //获取属性名
					 String attrName = attr.getName();
					 //获取属性值
					 String attrValue = attr.getValue();
					 //将属性值添加到bookEntity对象中
					 if ( attrName.equals("id")) {
						 bookEntity.setId(attrValue);
					 }
					 System.out.println("属性名:"+ attrName +"------属性值:"+ attrValue);
				 }
				 //对book节点的子节点的节点名和节点值的遍历
				 List<Element> bookChildren = book.getChildren();
				 for (Element child : bookChildren) {
					 String childName = child.getName();
					 String childValue = child.getValue();
					 System.out.println("节点名： "+childName+"属性值： "+ childValue);
					 if (childName.equals("name")) {
						 bookEntity.setName(childValue);
					 } else if (childName.equals("author")) {
						 bookEntity.setAuthor(childValue);
					 } else if (childName.equals("price")) {
						 bookEntity.setPrice(childValue);
					 } else if (childName.equals("language")) {
						 bookEntity.setLanguage(childValue);
					 } else if (childName.equals("year")) {
						 bookEntity.setYear(childValue);
					 } 
				 }
				 System.out.println("---------------结束解析第"+(bookList.indexOf(book) + 1)+"本书-----------");
				 booksList.add(bookEntity);
				 bookEntity = null;
				 
			 }
	//			 System.out.println(booksList.get(1).getName());
			} catch (FileNotFoundException e) {
				e.printStackTrace();
			} catch (JDOMException e) {
				e.printStackTrace();
			} catch (IOException e) {
				e.printStackTrace();
			}
		}
#### 生成XML文件 ####
	/**
	 * 生成xml文件
	 */
	public void createXML() {
		//1生成一个根节点
		Element rss = new Element("rss");
		//2为节点添加属性
		rss.setAttribute("version", "2.0");
		//3生成一个Document对象
		Document document = new Document(rss);
		Element channel = new Element("channel");
		rss.addContent(channel);
		Element title = new Element("title");
		channel.addContent(title);
		title.addContent( new CDATA("测试文本"));
		//4创建XMLOutputter对象
		XMLOutputter outputer = new XMLOutputter();
		//5利用outputer 将document对象转换成xml文档
		outputer.setFormat(Format.getPrettyFormat());
		try {
			outputer.output(document, new FileOutputStream("src/res/rssnews.xml"));
			
		} catch (FileNotFoundException e) {
			e.printStackTrace();
		} catch (IOException e) {
			e.printStackTrace();
		}
	}	
### DOM4J ###
DOM4J包的结构包括：

* Attribute    Attribute定义了XML的属性
* Branch     Branch为能够包含子节点的节点如XML元素(Element)和文档(Docuemnts)定义了一个公共的行为
* CDATA 	CDATA 定义了XML CDATA 区域
* CharacterData    ，，标识基于字符的节点。如CDATA，Comment, Text
* Comment    Comment 定义了XML注释的行为
* Document    定义了XML文档
* DocumentType    DocumentType 定义XML DOCTYPE声明
* Element    Element定义XML 元素
* ElementHandler    ElementHandler定义了 Element 对象的处理器
* ElementPath    被 ElementHandler 使用，用于取得当前正在处理的路径层次信息
* Entity    Entity定义 XML entity
* Node    Node为所有的dom4j中XML节点定义了多态行为
* NodeFilter    NodeFilter 定义了在dom4j节点中产生的一个滤镜或谓词的行为（predicate）
* ProcessingInstruction    ProcessingInstruction 定义 XML 处理指令.
* Text	Text 定义XML 文本节点.
* Visitor    Visitor 用于实现Visitor模式.
* XPathXPath 在分析一个字符串后会提供一个XPath 表达式
#### DOM4J的读取和写出 ####
	/**
	 * 向文件中写入内容
	 * @param file 需要写入内容的文件
	 */
	public static void write(File file, String dbName, String userName, String password){
		//1. 新建Document对象
		Document docu = DocumentHelper.createDocument();
		Element root = docu.addElement("databases");
		Element database = root.addElement("database");
		database.addElement("url").setText("jdbc:mysql://localhost:3306/" + dbName);
		database.addElement("user").setText(userName);
		database.addElement("password").setText(password);
		//2. 输出到文件
		try {
			BufferedWriter bw = new BufferedWriter(new OutputStreamWriter(new FileOutputStream(file), "utf-8"));
			docu.write(bw);
			bw.close();
		} catch (FileNotFoundException e) {
			e.printStackTrace();
		} catch (UnsupportedEncodingException e) {
			e.printStackTrace();
		} catch (IOException e) {
			e.printStackTrace();
		}
		
	}
	
	/**
	 * 读取xml文件的内容，并返回一个集合对象
	 * @param file 需要解析的文件
	 * @return 包含文件内容的HashMap集合
	 */
	public static HashMap<String, String> read(File file){
		if(! file.getName().endsWith(".xml")){
			throw new IllegalArgumentException("文件类型有误!");
		}
		HashMap<String, String> map = null;
		try {
			Document docu = new SAXReader().read(file);		//获得文档对象
			Element root = docu.getRootElement();		//获得根节点
			Element database = root.element("database");	
			String url = database.elementText("url");
			String userName = database.elementText("user");
			String password = database.elementText("password");
			//将值放入Map中
			map = new HashMap<>();
			map.put("url", url);
			map.put("user", userName);
			map.put("password", password);
		} catch (DocumentException e) {
			e.printStackTrace();
		}
		return map;
	}

### DOM概述 ###
DOM 是用与平台和语言无关的方式表示 XML 文档的官方 W3C 标准。DOM 是以层次结构组织的节点或信息片断的集合。这个层次结构允许开发人员在树中寻找特定信息。分析该结构通常需要加载整个文档和构造层次结构，然后才能做任何工作。由于它是基于信息层次的，因而 DOM 被认为是基于**树**或基于**对象**的。   

* 首先，由于树在内存中是持久的，因此可以修改它以便应用程序能对数据和结构作出更改。它还可以在任何时候在树中上下导航，而不是像 SAX 那样是一次性的处理。DOM 使用起来也要简单得多。
* 另一方面，对于特别大的文档，解析和加载整个文档可能很慢且很耗资源，因此使用其他手段来处理这样的数据会更好。
### SAX概述 ###
分析能够立即开始，而不是等待所有的数据被处理。而且，由于应用程序只是在读取数据时检查数据，因此不需要将数据存储在内存中。这对于大型文档来说是个巨大的优点。事实上，应用程序甚至不必解析整个文档；它可以在某个条件得到满足时停止解析。一般来说，SAX 还比它的替代者 DOM 快许多。
### JDOM概述 ###
JDOM的目的是成为 Java 特定文档模型，它简化与 XML 的交互并且比使用 DOM 实现更快。由于是第一个 Java 特定模型，JDOM 一直得到大力推广和促进。正在考虑通过“Java 规范请求 JSR-102”将它最终用作“Java 标准扩展”。
### DOM4J ###
它合并了许多超出基本 XML 文档表示的功能，包括集成的 XPath 支持、XML Schema 支持以及用于大文档或流化文档的基于事件的处理。它还提供了构建文档表示的选项，它通过 DOM4J API 和标准 DOM 接口具有并行访问功能。  

为支持所有这些功能，DOM4J 使用接口和抽象基本类方法。DOM4J 大量使用了 API 中的 Collections 类，但是在许多情况下，它还提供一些替代方法以允许更好的性能或更直接的编码方法。直接好处是，虽然 DOM4J 付出了更复杂的 API 的代价，但是它提供了比 JDOM 大得多的灵活性。
    
在添加灵活性、XPath 集成和对大文档处理的目标时，DOM4J 的目标与 JDOM 是一样的：针对 Java 开发者的易用性和直观操作。它还致力于成为比 JDOM 更完整的解决方案，实现在本质上处理所有 Java/XML 问题的目标。在完成该目标时，它比 JDOM 更少强调防止不正确的应用程序行为。
    
DOM4J 是一个非常非常优秀的Java XML API，具有性能优异、功能强大和极端易用使用的特点，同时它也是一个开放源代码的软件。如今你可以看到越来越多的 Java 软件都在使用 DOM4J 来读写 XML，特别值得一提的是连 Sun 的 JAXM 也在用 DOM4J.
### 选择 DOM 还是选择 SAX？ ###
DOM 采用建立**树形结构**的方式访问 XML 文档，而 SAX 采用的**事件模型**。  

DOM 解析器把 XML 文档转化为一个包含其内容的树，并可以对树进行遍历。用 DOM 解析模型的优点是编程容易，开发人员只需要调用建树的指令，然后利用navigation APIs访问所需的树节点来完成任务。可以很容易的添加和修改树中的元素。然而由于使用 DOM 解析器的时候需要处理整个 XML 文档，所以对性能和内存的要求比较高，尤其是遇到很大的 XML 文件的时候。由于它的遍历能力，DOM 解析器常用于 XML 文档需要频繁的改变的服务中。

**SAX 解析器采用了基于事件的模型**，它在解析 XML 文档的时候可以触发一系列的事件，当发现给定的tag的时候，它可以激活一个回调方法，告诉该方法制定的标签已经找到。SAX 对内存的要求通常会比较低，因为它让开发人员自己来决定所要处理的tag.特别是当开发人员只需要处理文档中所包含的部分数据时，SAX 这种扩展能力得到了更好的体现。
### JDOM 与 DOM 的区别? ###
首先，JDOM 仅使用具体类而不使用接口。这在某些方面简化了 API，但是也限制了灵活性。

第二，API 大量使用了 Collections 类，简化了那些已经熟悉这些类的 Java 开发者的使用。
JDOM 对于大多数 Java/XML 应用程序来说当然是有用的，并且大多数开发者发现 API 比 DOM 容易理解得多。JDOM 还包括对程序行为的相当广泛检查以防止用户做任何在 XML 中无意义的事。然而，它仍需要您充分理解 XML 以便做一些超出基本的工作（或者甚至理解某些情况下的错误）。这也许是比学习 DOM 或 JDOM 接口都更有意义的工作。  

JDOM 自身不包含解析器。它通常使用 SAX2 解析器来解析和验证输入 XML 文档（尽管它还可以将以前构造的 DOM 表示作为输入）。它包含一些转换器以将 JDOM 表示输出成 SAX2 事件流、DOM 模型或 XML 文本文档。
### 结论 ###
* XML文档是一个自我描述的数据集合
* XML的优点
 * 自我描述性
 * 可移植性
 *  以树结构描述数据
 *  提供可用于数据库的功能
*  XML的缺点
*  数据存储慢
*  缺少数据库的功能
*  在生产环境中将失效



