# 网络编程 #
## OSI模型 ##
* OSI参考模型（OSI/RM）    
全称是开放系统互连参考模型（Open System Interconnection Reference Model，OSI/RM）
它是由国际标准化组织（International Standard Organization，ISO）提出的一个网络系统互连模型。
* 层次结构：
 1. 物理层
 * 数据链路层
 * 网络层
 * 传输层
 * 会话层
 * 表示层
 * 应用层  
* 在这个OSI七层模型中，每一层都为其上一层提供服务、并为其上一层提供一个访问接口或界面。
### 物理层 ###
* **与传输媒体的接口,完成传输媒体上的信号和二进制数据间的转换**.
  
* 物理层的传输单位为比特（bit）。  
* 物理层定义了接口的机械特性,电气特性,功能和过程特性等.
  
* 例如插头,插座的几何尺寸,每根引脚的功能定义,逻辑[0]的[1]的电平定义,信号宽带定义等.
  属于物理层定义的典型规范代表包括：EIA/TIA RS-232、EIA/TIA RS-449、V.35、RJ-45等。
### 数据链路层 ###
* 该层的作用包括：物理地址寻址、数据的成帧、流量控制、数据的检错、重发,链路管理等。
* 在这一层，数据的单位称为帧（frame）。 
* 数据链路层协议的代表包括：SDLC、HDLC、PPP、STP、帧中继等。
### 网络层 ###
* 提供主机到主机的通信,其间可能存在多条能路,网络层将实现的功能包括:
   * 选择路由
   * 流量控制
   * 协议的转换
   * 分段和重组
   * 对用户的分组,字符等计数 等等

* 在这一层，数据的单位称为数据（packet）.
* 网络层协议的代表包括：IP、IPX、RIP、OSPF等。低三层的通信对象通常是路由器.
### 传输层 ###
* 提供端到端,应用到应用的通路.
* 传输层将把高层要求传输的数据分成若干个报文,报文和帧不一样,帧只有帧标记(开始标记和结果标记),而报文有信源和信宿的地址及端口.报文的顺序号,确定号等。

* 传输层协议的代表包括：TCP、UDP、SPX等
### 会话层 ###
* 会话层管理主机之间的会话进程，即负责建立、管理、终止进程之间的会话。
* 建立有关会话的机制,或双向对话,或对话时要有切换等.
* 会话层协议的代表包括：NetBIOS、ZIP（AppleTalk区域信息协议）等。
### 表示层 ###
* 表示层对上层数据或信息进行变换以保证一个主机应用层信息可以被另一个主机的应用程序理解。表示层的数据转换包括数据的加密、压缩、格式转换等。
* 表示层协议的代表包括：ASCII、ASN.1、JPEG、MPEG等。
### 应用层 ###
* 应用层为操作系统或网络应用程序提供访问网络服务的接口。
* 应用层协议的代表包括：Telnet、FTP、HTTP、SNMP等

## 数据封装过程 ##

* 当一台主机需要传送用户的数据（DATA）时，数据首先通过应用层的接口进入应用层。在应用层，用户的数据被加上应用层的报头（Application Header，AH），形成应用层协议数据单元（Protocol Data Unit，PDU），然后被递交到下一层-表示层。
* 表示层并不"关心"上层-应用层的数据格式而是把整个应用层递交的数据包看成是一个整体进行封装，即加上表示层的报头（Presentation Header，PH）。然后，递交到下层-会话层。
* 同样，会话层、传输层、网络层、数据链路层也都要分别给上层递交下来的数据加上自己的报头。它们是：会话层报头（Session Header，SH）、传输层报头（Transport Header，TH）、网络层报头（Network Header，NH）和数据链路层报头（Data link Header，DH）。其中，数据链路层还要给网络层递交的数据加上数据链路层报尾（Data link Termination，DT）形成最终的一帧数据。 
* 当一帧数据通过物理层传送到目标主机的物理层时，该主机的物理层把它递交到上层-数据链路层。数据链路层负责去掉数据帧的帧头部DH和尾部DT（同时还进行数据校验）。如果数据没有出错，则递交到上层-网络层。
* 同样，网络层、传输层、会话层、表示层、应用层也要做类似的工作。最终，原始数据被递交到目标主机的具体应用程序中
## TCP/IP模型 ##
ISO制定的OSI参考模型的过于庞大、复杂招致了许多批评。与此对照，由技术人员自己开发的TCP/IP协议栈获得了更为广泛的应用。
### TCP/IP层次结构 ###
* TCP/IP参考模型分为四个层次：**应用层、传输层、网络互连层和主机到网络层。**
* 在TCP/IP参考模型中，去掉了OSI参考模型中的会话层和表示层（这两层的功能被合并到应用层实现）。同时将OSI参考模型中的数据链路层和物理层合并为主机到网络层。 
#### 链路层 #### 
* 链路层，有时也称作数据链路层或网络接口层，
* 通常包括操作系统中的设备驱动程序和计算机中对应的网络接口卡。它们一起处理与电缆（或其他任何传输媒介）的物理接口细节。
* 负责数据帧的发送和接收，帧是独立的网络信息传输单元。网络接口层将帧放在网上，或从网上把帧取下来。 
### 网络互连层 ###
网络互连层是整个TCP/IP协议栈的核心。它的功能是把分组发往目标网络或主机。同时，为了尽快地发送分组，可能需要沿不同的路径同时进行分组传递。因此，分组到达的顺序和发送的顺序可能不同，这就需要上层必须对分组进行排序。  
网络互连层定义了分组格式和协议，即IP协议（Internet Protocol）。  
网络互连层除了需要完成路由的功能外，也可以完成将不同类型的网络（异构网）互连的任务。除此之外，网络互连层还需要完成拥塞控制的功能。
### 传输层 ###
在TCP/IP模型中，传输层的功能是使源端主机和目标端主机上的对等实体可以进行会话。在传输层定义了两种服务质量不同的协议。即：传输控制协议TCP（transmission control protocol）和用户数据报协议UDP（user datagram protocol）
  
TCP协议是一个面向连接的、可靠的.全双工协议。它将一台主机发出的字节流无差错地发往互联网上的其他主机。在发送端，它负责把上层传送下来的字节流分成报文段并传递给下层。在接收端，它负责把收到的报文进行重组后递交给上层。TCP协议还要处理端到端的流量控制，以避免缓慢接收的接收方没有足够的缓冲区接收发送方发送的大量数据。
  
UDP协议是一个不可靠的、无连接协议，主要适用于不需要对报文进行排序和流量控制的场合
### 应用层 ###
* TCP/IP模型将OSI参考模型中的会话层和表示层的功能合并到应用层实现。应用层面向不同的网络应用引入了不同的应用层协议。
* 有基于TCP协议的，
 * 文件传输协议（File Transfer Protocol，FTP）
 * 虚拟终端协议（TELNET）
 * 超文本链接协议（Hyper Text Transfer Protocol，HTTP），
* 也有基于UDP协议的，
 * 简单网络管理协议（Simple Network Management Protocol，SNMP）
 * 简单文件传输协议（Trivial File Transfer Protocol，TFTP)
 * 网络时间协议（Network Time Protocol，NTP）
### TCP/IP协议栈 ###
T C P / I P协议族是一组不同的协议组合在一起构成的协议族。尽管通常称该协议族为T C P / I P，但T C P和I P只是其中的两种协议而已（该协议族的另一个名字是I n t e r n e t协议族(Internet Protocol Suite)）
### 网络层和传输层 ###
* 在8 0年代，网络不断增长的原因之一是大家都意识到只有一台孤立的计算机构成的“孤岛”没有太大意义，于是就把这些孤立的系统组在一起形成网络。随着这样的发展
* 到了9 0年代，我们又逐渐认识到这种由单个网络构成的新的更大的“岛屿”同样没有太大的意义。于是，人们又把多个网络连在一起形成一个网络的网络，或称作互连网( i n t e r n e t )。一个互连网就是一组通过相同协议族互连在一起的网络。
## 网络互联 ##
* 连接网络的另一个途径是使用网桥。网桥是在链路层上对网络进行互连，而路由器则是在网络层上对网络进行互连。网桥使得多个局域网（ L A N）组合在一起，这样对上层来说就好像是一个局域网。
* TCP /IP倾向于使用路由器而不是网桥来连接网络.
## 域名系统 ##
* 尽管通过I P地址可以识别主机上的网络接口，进而访问主机，但是人们最喜欢使用的还是主机名。在T C P / I P领域中，域名系统（ D N S）是一个分布的数据库，由它来提供I P地址和主机名之间的映射信息。
* 现在，我们必须理解，任何应用程序都可以调用一个标准的库函数来查看给定名字的主机的I P地址。类似地，系统还提供一个逆函数—给定主机的I P地址，查看它所对应的主机名。
* 大多数使用主机名作为参数的应用程序也可以把I P地址作为参数。
*  ARP协议是“Address Resolution Protocol”（地址解析协议）的缩写。在局域网中，网络中实际传输的是“帧”，帧里面是有目标主机的MAC地址的。在以太网中，一个主机要和另一个主机进行直接通信，必须要知道目标主机的MAC地址。但这个目标MAC地址是如何获得的呢？它就是通过地址解析协议获得的。所谓“地址解析”就是主机在发送帧前将目标IP地址转换成目标MAC地址的过程。ARP协议的基本功能就是通过目标设备的IP地址，查询目标设备的MAC地址，以保证通信的顺利进行。

**如何查看ARP缓存表: arp -a**
## TCP/IP ##
* 在T C P / I P协议族中，网络层I P提供的是一种不可靠的服务。也就是说，它只是尽可能快地把分组从源结点送到目的结点，但是并不提供任何可靠性保证。
### TCP ###
* TCP是一个**可靠的、面向连接**的协议。它可以保证数据从连接的一方传递到另一方，并且发送数据的顺序和所接收数据的顺序一致。当应用程序需要一个可靠的、点对点的连接时，可以使用TCP。
* 为了提供这种可靠的服务， T C P采用了超时重传、发送和接收端到端的确认分组等机制。
### UDP ###
用户数据报协议UDP是一种**不可靠**的通信协议，没有检测错误的机制，也不重发丢失的数据。  
接收到的数据包的顺序可能与发送的数据包的顺序不一致。  
采用UDP进行通信时，**事先不需要建立连接**。   
而采用TCP进行通信时，首先要建立一个连接。TCP的通信质量比UDP高，UDP的开销比TCP小。
### 端口和IP ###
* 在网络上可以用IP地址来唯一的标识一台计算机。IP地址（IPv4）是四个用点隔开的数字，总共32位，每个数字8位（表示范围：0～255），例如：192.168.10.22。（IPv6地址有128位，地址范围更大）
* 端口port与IP地址一起可以为网络的应用程序之间提供一种地址标识功能。同一台计算机上可能有多个服务程序，每个服务程序在相应的port提供服务。
* 客户端程序要和服务程序交互，首先要找到服务程序所在的机器（可以通过IP地址），然后在这台机器上找到服务程序（通过port）。在一台服务器上，可能有很多服务程序，每个服务程序对应与一个不与其他服务冲突的port
* 客户端程序必须事先知道它所请求的服务程序对应的端口号。
* port通常称为握手点handshake point，它被客户用来定位服务器计算机上的服务应用程序。
* 端口号范围：0～65535。可以是范围中的任何一个数字。通常，OS将1024以下的端口号保留给系统服务用。
* 建立连接服务程序在相应的port监听是否有连接Connection。客户端程序尝试与服务程序。连接建立以后，可以通过连接传输数据，在处理数据时，可以使用与IO处理相同的Java编程模型

# 网络编程 #
* 网络编程的目的就是指直接或间接地通过网络协议与其他计算机进行通讯。
* 网络编程中有两个主要的问题.
 * 一个是如何准确的定位网络上一台或多台主机，
 * 另一个就是找到主机后如何可靠高效的进行数据传输。
 * 在TCP/IP协议中IP层主要负责网络主机的定位，数据传输的路由，由IP地址可以唯一地确定Internet上的一台主机。而TCP层则提供面向应用的可靠的或非可靠的数据传输机制，这是网络编程的主要对象，一般不需要关心IP层是如何处理数据的。
## TCP/UDP ##
* 尽管TCP/IP协议的名称中只有TCP这个协议名，但是在TCP/IP的传输层同时存在TCP和UDP两个协议。 
* TCP是Tranfer Control Protocol的简称，是一种面向连接的保证可靠传输的协议。通过TCP协议传输，得到的是一个顺序的无差错的数据流。发送方和接收方的成对的两个socket之间必须建立连接，以便在TCP协议的基础上进行通信，当一个socket（通常都是server socket）等待建立连接时，另一个socket可以要求进行连接，一旦这两个socket连接起来，它们就可以进行双向数据传输，双方都可以进行发送或接收操作。
* UDP是User Datagram Protocol的简称，是一种无连接的协议，每个数据报都是一个独立的信息，包括完整的源地址或目的地址，它在网络上以任何可能的路径传往目的地，因此能否到达目的地，到达目的地的时间以及内容的正确性都是不能被保证的。 
* 使用UDP时，每个数据报中都给出了完整的地址信息，因此无需要建立发送方和接收方的连接。对于TCP协议，由于它是一个面向连接的协议，在socket之间进行数据传输之前必然要建立连接，所以在TCP中多了一个连接建立的时间。
* 使用UDP传输数据时是有大小限制的，每个被传输的数据报必须限定在64KB之内。而TCP没有这方面的限制，一旦连接建立起来，双方的socket就可以按统一的格式传输大量的数据。UDP是一个不可靠的协议，发送方所发送的数据报并不一定以相同的次序到达接收方。而TCP是一个可靠的协议，它确保接收方完全正确地获取发送方所发送的全部数据
* 总之，TCP在网络通信上有极强的生命力，例如远程连接（Telnet）和文件传输（FTP）都需要不定长度的数据被可靠地传输。相比之下UDP操作简单，而且仅需要较少的监护，因此通常用于局域网高可靠性的分散系统中client/server应用程序。
* 既然有了保证可靠传输的TCP协议，为什么还要非可靠传输的UDP协议呢？主要的原因有两个。
 * 一是可靠的传输是要付出代价的，对数据内容正确性的检验必然占用计算机的处理时间和网络的带宽，因此TCP传输的效率不如UDP高。
 * 二是在许多应用中并不需要保证严格的传输可靠性，比如视频会议系统，并不要求音频视频数据绝对的正确，只要保证连贯性就可以了，这种情况下显然使用UDP会更合理一些。
## Socket简述 ##
* **socket是进程之间通信的抽象连接点**。客户程序和服务程序通过一个双向的通信连接实现数据交换，这个双向通路的每一端就是一个socket。
* 现实生活中，人们可以通过电话进行交流。我们可以把打电话的双方看作客户程序和服务程序，电话之间的连线是一个双向的通信链路，链路每一端的电话机可以看成是一个socket。
### Socket种类 ###
目前有两种socket：**流式socket、数据报式socket**。  
流式socket提供了双向的、有序的、无重复的数据流服务。TCP是一种流式socket协议；UDP是一种数据报式socket协议。数据报式socket支持双向的数据流，但不能保证有序、无重复。
## URL ##
URL是**统一资源定位符Uniform Resource Locator**的简称，以一个字符串的形式表示Internet上某一资源的位置。URL地址由两部分组成：协议名和资源名，两者用“ : ”隔开。协议名指出了访问该资源所使用的网络协议，如http、ftp等。资源名是网络资源的完整地址，包括主机名、端口号、文件名和文件的一个引用。

### URL类 ###
java.net包中有一个URL类，可以通过URL类创建的对象来代表一个网络资源。
类URL的构造方法：

	public URL(String s); s是表示URL地址的字符串。
	例如： new URL(“http://www.sun.com/”);

	public URL(URL context,String s); 例如：
	URL u1=new URL(“http://www.sun.com/”);
	URL u2=new URL(u1, “index.html”);
	public URL(String protocol,String host,String file);
	public URL(String protocol,String host,int port,String file);     
	例如：URL u=new URL(“http”, “www.sun.com”，80，“index.html”);

URL类的构造方法声明抛出(throws)异常MalformedURLException(将异常抛给调用构造方法的代码)。所以我们必须在调用URL构造方法的地方对异常进行处理.
### URL属性 ###
一个URL对象生成后，其属性是不能被改变的，但是我们可以通过类URL所提供的方法来获取这些属性:

	public String getProtocol() 获取该URL的协议名。
	public String getHost() 获取该URL的主机名。
	public int getPort() 获取该URL的端口号，如果没有设置端口，返回-1。
	public String getFile() 获取该URL的文件名。
	public String getRef() 获取该URL在文件中的相对位置。
	public String getQuery() 获取该URL的查询信息。
	public String getPath() 获取该URL的路径
	public String getAuthority() 获取该URL的权限信息
	public String getUserInfo() 获得使用者的信息
	public String getRef() 获得该URL的锚 

### 通过URL对象可以访问网络资源 ###
URL提供了openStream( )方法，该方法与指定的URL地址建立连接并返回一个InputStream类的对象，因此可以使用InputStream类的方法读取数据，和普通的文件处理一样方便，只是读取的文件不是在本地计算机上，而是在网络上。

其定义为：

	InputStream openStream();　
	方法openSteam()与指定的URL建立连接并返回InputStream类的对象以从这一连接中读取数据。
### 从URL读取网络资源 ###
	public class URLReader {
		public static void main(String[] args) throws     Exception { 
			URL tirc =  new    URL("http://www.tirc1.cs.tsinghua.edu.cn/"); 　BufferedReader in = new BufferedReader(new InputStreamReader(tirc.openStream()));
			String inputLine;
			while ((inputLine = in.readLine()) != null) 　　　　　　　　　　　　　　　　　　　　　　	System.out.println(inputLine); 
			in.close(); //关闭输入流
	　　}
	}
### 通过URLConnection连接www ###
* URL只能从网络读取数据，如果还想发送给服务器一些数据，就得用URLConnection.
* 类URLConnection也在包java.net中定义，它表示Java程序和URL在网络上的通信连接。当与一个URL建立连接时，首先要在一个URL对象上通过方法openConnection()生成对应的URLConnection对象。

	Try{
		URL netchinaren = new URL ("http://blog.163.com");
		URLConnectonn tc = netchinaren.openConnection();
	}catch(MalformedURLException e){ //创建URL()对象失败
		…
	}catch (IOException e){ 
		//openConnection()失败
		…
	}
### InetAddress类 ###
* Java通过InetAddress对象存储网络计算机的Internet地址，该对象含有与网络编程有关的许多变量和方法。有三个方法可以用来创建InetAddress实例：

		InetAddress i＝InetAddress.getLocalhost();
	    getLocalhost( )返回代表本地主机的   InetAddress对象。
	
		InetAddress  i= InetAddress.getByName(“java.sun.com”);
	     getByName(hostname)返回由hostname所指定机器的InetAddress对象，如果找不到hostname机器，则该方法抛出UnknownHostException。
	
		InetAddress i= InetAddress.getAllByName(“java.sun.com”);
		可以用同样的名字代表一组机器。getAllByName(hostname)返回一组具有相同名字的InetAddress对象，如果一台机器都没找到，则方法抛出UnknownHostException。

* 在InetAddress类中，提供了一些常用的方法：

		public String getHostName();返回表示InetAddress对象主机名的字符串。
		public byte[ ] getAddress();
		     返回InetAddress对象的地址。
		public String getHostAddress();
		     返回InetAddress对象的Internet地址。

## Socket编程 ##
* Java提供了URL类用来在一个相对较高的层次上进行网络通讯，以实现对Internet上资源的访问。但有时程序需要较低层次的网络通信。如客户机/服务器应用程序以及某些特殊协议的应用
* 在各种网络的C/S应用中，客户机与服务器之间的通信组件是多种多样的，大部分通信组件内最低层的核心通信机制都是使用传输层接口的socket机制来实现的。  
* socket是在两个应用程序之间用来进行双向数据传输的网络通信端点，一般由一个地址加一个端口号来识别。每个服务程序在一个众所周知的端口提供服务
* UDP协议不能保证数据包以指定的顺序到达。数据包可能丢失，也可能重复，甚至可能无序到达。因此，如果使用UDP，程序员需要投入大量额外的编程工作，以应对这些问题。UDP适用于不要求错误检查和可靠性的网络应用程序，可靠性差，但速度快。
* 在网络编程时，大多数的时候，我们采用TCP，偶尔才会使用UDP。TCP提供了一个可靠的、面向连接的通信通道

### 服务端 ###

	import java.io.IOException;
	import java.net.ServerSocket;
	import java.net.Socket;
	import java.util.ArrayList;
	
	/**
	 * 服务端
	 */
	public class Server {
		private ArrayList<Socket> sockets ;	//客户端连接对象
		
		public static void main(String[] args) {
			Server server = new Server();
			server.start(9900);
		}
		
		/**
		 * @return the sockets
		 */
		public ArrayList<Socket> getSockets() {
			return sockets;
		}
	
		/**
		 * @param sockets the sockets to set
		 */
		public void setSockets(ArrayList<Socket> sockets) {
			this.sockets = sockets;
		}
	
		/**
		 * 开启服务器
		 */
		public void start(int port){
			System.out.println("服务器已经开启！");
			ServerSocket serverSocket = null;
			try {
				serverSocket = new ServerSocket(port);
				sockets = new ArrayList<>();
				while(true){
					Socket socket = serverSocket.accept();
					System.out.println(socket.getInetAddress().getHostName() + "  连接到服务器!");
					sockets.add(socket);
					ServerThread servetThread = new ServerThread(socket, sockets);
					Thread thread = new Thread(servetThread);
					thread.start();
				}
			} catch (IOException e) {
				e.printStackTrace();
			}
		}
	}

### 服务端线程 ###
	import java.io.BufferedReader;
	import java.io.IOException;
	import java.io.InputStreamReader;
	import java.io.PrintWriter;
	import java.net.Socket;
	import java.net.SocketException;
	import java.util.ArrayList;
	
	/**
	 * 服务器线程
	 */
	public class ServerThread implements Runnable {
		private Socket socket;  //当前连接对象
		private ArrayList<Socket> sockets;  //所有连接对象
		
		/**
		 * 默认构造器
		 */
		public ServerThread() { }
		
		/**
		 * 根据当前连接和客户端集合创建服务线程
		 * @param socket 当前连接
		 * @param sockets 客户端集合
		 */
		public ServerThread(Socket socket, ArrayList<Socket> sockets) {
			super();
			this.socket = socket;
			this.sockets = sockets;
		}
	
		@Override
		public void run() {
			BufferedReader socketReader =null;
			PrintWriter writer = null;
			while(true){
				try {
					//获得当前socket的信息
					socketReader = new BufferedReader(new InputStreamReader(socket.getInputStream()));
					String message = socketReader.readLine();
					//将信息发送给所有的客户端
					for(Socket s : sockets){
						if(s == null){
							sockets.remove(s);
							continue;
						}
						writer = new PrintWriter(s.getOutputStream());
						writer.println(message);
						writer.flush();
					}
				} catch (SocketException e) {
	//				e.printStackTrace();
				} catch(IOException e){
					e.printStackTrace();
				}
			}
		}
	
	} 

### 客户端 ###
	import java.io.BufferedReader;
	import java.io.IOException;
	import java.io.InputStreamReader;
	import java.io.PrintWriter;
	import java.net.Socket;
	
	public class Client {
	
		public static void main(String[] args) throws  IOException {
			Socket socket = new Socket("localhost", 9000);
			BufferedReader br = new BufferedReader(new InputStreamReader(System.in)); 
			PrintWriter pw = new PrintWriter(socket.getOutputStream());
			BufferedReader brServer = new BufferedReader(new InputStreamReader( socket.getInputStream()));
			
			while(true){
				System.out.println("请输入数据:");
				String output = br.readLine();
				if("exit".equals(output)){
					break;
				}
				pw.println(output);
				pw.flush();
				System.out.println("服务器反馈信息:" + brServer.readLine());
			}
			
			pw.close();
			br.close();
			brServer.close();
			socket.close();
		}
	
	}
### TCP Socket通信程序的开发步骤 ###
1. 初始化服务器，建立serversocket对象，等待客户机的连接请求。
2. 初始化客户机，建立socket对象，向服务器发出连接请求。
3. 服务器响应客户机，建立连接。
4. 客户机向服务器发送请求数据。
5. 服务器接受客户机请求数据
6. 服务器处理数据，并把处理结果返回给客户机。
7. 客户机接收服务器返回的结果。
8. 重复4～7步，直到客户机结束对话为止。
9. 中断连接，结束通信。

java.net包中的Socket和ServerSocket类分别用于在客户机和服务器上创建和管理socket。
