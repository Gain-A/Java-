# IO #
## File类 ##
File类有一个欺骗性的名字——通常会认为它对付的是一个文件，但实情并非如此。它既代表一个特定文件的名字，也代表目录内一系列文件的名字。若代表一个文件集，便可用list()方法查询这个集，返回的是一个字串数组。之所以要返回一个数组，而非某个灵活的集合类，是因为元素的数量是固定的。而且若想得到一个不同的目录列表，只需创建一个不同的File对象即可。事实上，“FilePath”（文件路径）似乎是一个更好的名字。
### 目录列表器 ###
现在假设我们想观看一个目录列表。可用两种方式列出File对象
* 在不含自变量（参数）的情况下调用list()，会获得File对象包含的一个完整列表
* 然而，若想对这个列表进行某些限制，就需要使用一个“目录过滤器”，该类的作用是指出应如何选择File对象来完成显示
### 检查与创建目录 ###
1. File类并不仅仅是对现有目录路径、文件或者文件组的一个表示
2. 亦可用一个File对象新建一个目录，甚至创建一个完整的目录路径——假如它尚不存在的话
3.  亦可用它了解文件的属性（长度、上一次修改日期、读／写属性等），检查一个File对象到底代表一个文件还是一个目录，以及删除一个文件等等
## Java IO ##
大多数应用程序都需要与外部设备进行数据交换，最常见的外部设备包含磁盘和网络，IO就是指应用程序对这些**设备**的数据**输入与输出**。  
在程序中，键盘被当作输入文件，显示器被当作输出文件使用。Java语言定义了许多类专门负责各种方式的输入输出，这些类都被放在**java.io包**中。
### IO 读写过程 ###
* 读的过程

		open a stream 
		while more information 	
			read information
		close the stream 
* 写的过程
	
		open a stream 
		while more information 	
			write information
		close the stream
### IO操作的类分类 ###
* 在Java中，IO流的操作主要根据操作的数据类型分为两类**字符流和字节流**
* 以字节为导向的stream,表示以字节为单位从stream中读取或往stream中写入信息
* 以Unicode字符为导向的stream，表示以Unicode字符为单位从stream中读取或往stream中写入信息
 * Unicode（统一码、万国码、单一码）是一种在计算机上使用的字符编码。它为每种语言中的每个字符设定了统一并且唯一的二进制编码，以满足**跨语言、跨平台进行文本转换、处理的要求 **
#### InputStream ####
	InputStream
		FileInputStream
		PipedInputStream
		FilterInputStream
			LineNumberInputStream
			DataInputStream
			BufferedInputStream
			PushbackInputStream
		ByteArrayInputStream
		SequenceInputStream
		StringBufferInputStream
		ObjectInputStream
#### OutputStream ####
	OutputStream
		FileOutputStream
		PipedOutputStream
		FilterOutputStream
			DataOutputStream
			BufferedOutputStream
			PrintStream
		ByteArrayOutputStream
		ObjectOutputStream
#### Reader ####
	Reader
		BufferedReader
			LineNumberReader
		CharArrayReader
		InputStreamReader
			FileReader
		FilterReader
			PushbackReader
		PipedReader
		StringReader
#### Writer ####
	Writer
		BufferedWriter
		CharArrayWriter
		OutStreamWriter
			FileWriter
		FilterWriter
		PipedWriter
		StringWriter
### Reader/Writer和InputStream/OutputStream ###
* Reader和InputSream分别为字符和字节定义了一下相似的API。
 * Reader:
  		* int read()
  		* int read(char cbuf[])
  		* int read(char cbuf[], int offset, int length)
 * InputSteam也定义了一些类似的方法:
		* int read()
		* int read(byte[] buf)
		* int radd(byte[] buf, int offset, int length)
* Writer和OutputStream分别为字符和字节定义了相似的API
 * Writer:
 		* int write(int c)
 		* int write(char[] buf)
 		* int write(char[] buf, int offset, int length)
 * OutputStream:
 		* int write(int c)
 		* int write(byte[] buf)
 		* int wirte(byte[] buf, int offset, int length)
### Reader/Writer用途 ###
* Reader和Writer用户国际化，字符流仅支持8位字节流，不能很好的支持16位的Unicode字符
* Unicode字符用于国际化。Reader和Writer设计操作比旧类库更快
* 优先使用Reader和Writer，但有些情况下必须使用InputStream和OutputStream 

### File流类 ###
* FileInputStream 用于从文件读取信息，代表文件名的一个字符串，或者File或FileDescriptor对象作为数据源使用。  
通过将其同一个FileterInputStream对象连接通过一个有用的接口。  
* FileOutputStream将信息发给一个文件，同一个String表示文件名，或选用一个File或FileDescriptor对象用于指出数据的目的地。  
若将其同FilterOutputStream对象连接在一起，可提供一个有用的接口
### 字节数组流 ###
* ByteArrayInputStream允许内存中的一个缓冲区作为InputStream使用，从中提取字节缓冲区作为数据源使用。  
通过将其同一个FilterInputStream对象连接可提供一个有用的接口。
* ByteArrayOutputStream在内存中创建一个缓冲区。我们发送给流的所有数据都会置入这个缓冲区。可选缓冲区的初始大小，用户指出数据的目的地。
### 过滤流 ###
* 过滤流总是和其它的流配合使用，在其它的流上提供一些额外的功能。（修饰器模式）
* FilterInputStream和FilterOuputStream(这两个名字十分不直观)提供了相应的装饰器接口，用于控制一个特定的输入流（InputStream)或者输出流(OutputStream)。它们分别是从InputStream和OutputStream衍生出来的。
* 它们都属于抽象类，在理论上为我们与一个流的不同通信手段狗提供了一个通用的接口。  
事实上，FilterInputStream和FilterOutputStream只是简单的模仿了自己的基类，它们是一个装饰器的基本要求。
### DataInputStream ###
DataInputStream允许我们读取不同的基本数据类型，以及String对象（所有的方法都以read开头，比如readByte,readFloat等等）。  
伴随对应的DataOutputStream，我们可通过数据“流”将基本数据类型的数据从一个地方搬到另一个地方。  
若读取块内的数据，并自己进行解析，就不需要用到DateInputStream。但在其他许多情况下，我们一般都想用它对自己的数据进行自动格式化。
### DataOutputStream ###
DataOutputStream对各个基本数据类型以及String对象进行格式化，并将其置入一个数据“流”中，以便任何机器上的DataInputStream都能正常的读取它们。所有方法都以write开头，一如writeByte，writeFloat
### DataInputStream/DataOutputStream的使用 ###
* DataInputStream像其他流一样，必须和另外的一个InputStream连接起来。
### PrintStream ###
* 若想进行一些真正的格式化输出，比如输出到控制台，请使用PrintStream。利用它可以打印所有的基本数据类型和String类型对象，并可采用一种便于查看的格式。  
* 这与DataOutputStream正好相反，后者的目标是将那些数据置入一个数据流中，以便DataInputStream能够方便的重构它们。  
* **System.out**是一个静态PrintStream对象。
* PrintStream内有两个重要的方法是print(),println()，它们已进行了覆盖处理，可打印出所有的数据类型。  
print()和println()之间的差异是后者在操作完毕后会自动添加一个新的行。
### BufferedOutputStream ###
* BufferedOutputStream属于一种“修改器”，用于指示数据流使用缓冲技术，使自己不必每次都向流内物理性地写入数据。通常都应将它用于文件处理和控制器IO。
### RandomAccessFile ###
RandomAccessFile用于包含了已知长度记录的文件，以便于我们能用seek()从一条记录移至另一条记录；实现随机读取或修改那些记录。各记录的长度并不一定相同；只知道它们有多大以及置于文件何处即可。  
RandomAccessFile不属于InputStream或者OutputStream分层结构的一部分。除了恰巧实现了DataInput以及DataOutput接口之外，它们与那些分层结构并没有什么关系。不管在哪种情况下，它都是独立运作的，作为Object的一个直接继承人使用。  
从根本上说，RandomAccessFile类似DataInputStream和DataOutputStream的联合使用。其中getFilePinter()用于了解当前的文件的什么地方，seek()方法用于移至文件的一个新地点，而length()用于判断文件的最大长度。此外，构建器要求使用另一个自变量，指出自己只是随机读（"r"），还是读写兼具（"rw"）。这里没有提供对“只读文件”的支持。
## Java 1.1的IO流 ##
与原来的IO流库相比，经常要对新IO流进行层次更多的封装。同样的，这也属于装饰器方案的一个缺点--需要为额外的灵活性付出代价。  
1. 在老式层次结构里加入了新类，所以Sun公司明显不会放弃老式数据流。
2. 在许多情况下，我们需要与新结构中的类联合使用老结构中的类。  
为了达到这个目的，需要使用一些“桥”类：  
InputStreamReader将一个InputStream转化为Reader，OutputStreamWriter将一个OutputStream转化为Writer。之所以在Java1.1里添加了Reader和Writer层次，最重要的原因便是国际化的需求。老式IO流层次结构只支持8位字节流，不能很好的控制Unicode字符。  
由于Unicode主要面向的是国际化的支持，所以添加了Reader和Writer层次，以提供对所有IO操作中的Unicode的支持。除此之外，新库也对速度进行了优化，可比旧库更快的运行。
### 数据的发起和接收 ###
Java 1.0的几乎所有IO流都有对应的1.1类，用于提供內建的Unicode管理。似乎最重要的事情就是“全部使用新类，再也不要用旧的”，但实际情况并没有那么简单。有些时候，由于受到库设计的一些限制，我们不得不使用Java 1.0的IO流类。特别需要指出的是，在旧流库的基础上新加了java.util.zip库，它们依赖旧的流组件。所以最明智的做法是“尝试性”的使用Reader和Writer类。若代码不能通过编译，便知道必须换回老式库。
### 修改流数据的行为 ###
在Java 1.0中，数据流通过FilterInputStream和FilterOutputStream的“装饰器”（Decorator）子类适应特定的需求。Java 1.1的IO流沿用了这一思想，但没有采用所有装饰器都从相同“filter”基础类中衍生这一做法。  
### 未改变的类 ###
* DataOutputStream
* File
* RandomAccessFile
* SequenceInputStream
### 重导向标准IO ###
Java 1.1在System类中添加了特殊的方法，允许我们重定向标准输入、输出以及错误IO流。此时要用到下述简单的静态方法调用：  
setIn(InputStream)  
setOut(PrintStream)  
setErr(PrintStream)  
如果突然要在屏幕上生成大量输出，而且滚动的速度快于人们的阅读速度，输出的重定向就显得特别的有用。在一个命令行程序中，如果想重复的测试一个特定的用户输入序列，输入的重定向也显得特别有价值。
### 对象序列化 ###
Java 1.1增加了一种有趣的特性，名为“对象序列化”（Object Serialization）。它面向那些实现了Serializable接口的对象。可将它们转化成一系列字节，并可在以后完全恢复会原来的样子。这一过程亦可通过网络进行。这意味着序列化机制能自动补偿操作系统之间的差异。换句话说，可以先在Windows机器上创建一个对象，对其序列化，然后通过网络发给一台Unix机器，然后在那里准确无误地重新“装配”。不必关心数据在不同机器上如何表示，也不必关心字节的顺序或者其他任何细节。  
为序列化一个对象，首先要创建某些OutputStream对象，然后将其封装到ObjectOutputStream对象内。此时，只需要调用writeObject()即可完成对象的序列化，并将其发送给OutputStream。相反的过程是将一个InputStream封装到ObjectInputStream中，然后调用readObject()。和往常一样，我们最后获得的是指向一个上溯造型Object的句柄，所以必须下溯造型，以便能够直接设置。  
我们注意到对象的序列化并不属于新的Reader和Writer层次结构的一部分，而是沿用老式的InputStream和OutputStream结构。所以在一些特殊的场合下，不得不混合使用两种类型的层次结构。
#### 序列化的控制 ####
* 通过实现Externalizable接口，用它代替Serializable接口，便可控制序列化的具体过程。这个Externalizable接口拓展了Serializable，并增添了两个方法：writeExternal()和readExternal()。在序列化和重新装配的过程中，会自动调用这两个方法，以便我们执行一些特殊操作。
* transient关键字
控制序列化的过程中，可能有一个特定的子对象不愿让Java的序列化机制自动保存和恢复。一般地，若那个子对象包含了不想序列化的敏感信息（如密码），就会面临这种情况。即使那种信息在对象中具有“private”属性，但一旦经序列化处理，人们就可以通过读取一个文件，或者拦截网络传输得到它。为了防止对象的敏感信息被序列化，一个办法是将自己的类实现为Externalizable。这样一来没有任何东西可以自动序列化，只能在writeExternal()明确序列化那些需要的部分。然而，若操作的是一个Serilizable对象，所有序列化操作都会自动进行。为解决这个问题，可以用transient逐个字段的关闭序列化，它的意思是需要自动机制保存或回复它。

    




