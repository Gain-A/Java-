# 集合Collection #
* 集合类存放于java.util包中
* 集合类存放的都是对象，即对象的引用(reference)
* 主要类型：
 * Set(集)：无法拥有重复元素，使用自己内部的一个排列机制
 * List(列表):必须以一定次序来持有各元素(以元素插入次序来放置元素)
 * Map(映射):一群成对的key-value对象，也是使用自己内部排列机制
* 其中Set和List集合均派生自Collection接口 
## 关系图 ##
	Collection
		List
			LinkedList
			ArrayList
			Vector
				Stack
		Set
			HashSet
			TreeSet
	
	Map	
		Hashtable	//注意是Hashtable，早起命名不规范引起的
		HashMap
		TreeMap
## Collection接口 ##
* 最上层接口
* 基本方法(增删改查)  

		boolean add(Object obj)
		boolean remove(Object obj)
		boolean contains(Object obj)
		void clear()
虽返回的是boolean，但不是表示的添加成功与否，因为Collection规定：一个集合拒绝添加这个元素，无论什么原因，都必须抛出异常。  
这个返回值的意义是add()执行后，集合的内容是否更改了(元素有无数量、位置变化)。类似的addAll,remove,removeAll,remainAll也是一样的。
### iterator ###
* 迭代器	(iterator),它是一个对象，其职责是走访以及选择序列(sequence)中的一串对象
* 使用迭代器：
 * 调用iterator(),要求容器交给你一个Iterator。当你第一次调用Iterator的next()时，它将返回序列中的第一个元素
 * 调用next()取的序列中的下一个元素，如果达到集合结尾，则抛出NoSuchElementException
 * 调用hasNext()检查序列中是否还有其他元素
 * 调用remove()移去迭代器最新传回的元素，本方法**必须跟在一个元素的访问后执行**。如果上次访问后，集合已经被修改，方法将抛出IllegalStateException
* Iterator中删除操作对底层Collection也有影响
 * 如果在用Iterator遍历集合时，另一个线程修改底层集合，Iterator会抛出ConcurrentModificationException(并发修改异常)
* Iterator遍历所有元素:
		
		Iteratro it = collection.iterator();
		while(it.hasNext()){
			Obejct obj = it.next(); //得到下一个元素
		}
## List接口 ##
列表的主要特征是其对象以线性特征存储，没有特定顺序，只有一个开头和结尾。当然，它与根本没有顺序的集是不同的。  
列表在数据结构中分别表现为：数组和向量、链表、堆栈、队列。
### ArrayList类 ###
* ArrayList实现了大小可变的的数组。它允许添加所有元素，包括null。
* size,isEmpty,get,set方法运行时间为常数。但是add方法开销为分摊的常数，添加n个元素需要O(n)的时间。其它方法运行时间为线性。
* 每个ArrayList实例都有一个容量(capacity)，即用于存储数组的大小。这个容量可随着添加新元素而自动增加，但是增长算法没有定义。当需要插入大量元素时，在插入前可以调用ensureCapacity方法来增加ArrayList的容量以提高插入效率。
### LinkedList类 ###
LinkedList类添加了一些处理列表两端元素的方法。

	void addFirst(Object o)	将对象o添加到列表的开头
	void addLast(Object o) 	将对象o添加到列表的末尾
	Object getFirst()		返回列表开头的元素
	Object getLast()		返回列表末尾的元素
	Object removeFirst()	删除并返回列表开头的元素
	Object removeLast()		删除并返回列表结尾的元素
### ArrayList和LinkedList区别 ###
* ArrayList封装了一个动态再分配的Object[]数组
* LinkedList是链表结构
* 当需要频繁添加、删除元素时，最好用LinkedList
* 当需要频繁查询和修改元素时，最好用ArrayList
### Vector ###
* Vector非常类似ArrayList，但是Vector是**线程同步的**。
* 当一个Iterator被创建而且正在被使用，另一个线程改变了Vector的状态（例如，添加或删除了一些元素），这时调用Iterator的方法时将抛出**ConcurrentModificationException**，因此必须捕获该异常。 

### Vector和ArrayList区别 ###
* Vector类中的所有方法都是线程同步的，两个线程迸发访问Vector对象将是安全的，但只有一个线程访问Vector对象时，因为源程序仍调用了同步方法，需要额外的监视检查，运行效率要低。
* ArrayList类中的所有方法是异步的，所以在没有多线程安全问题时，最好用ArrayList，程序的效率会高些。在有线程安全问题，且我们的程序又没有自己处理(自己处理是指对调用ArrayList的代码或方法加上同步处理)时，只能用Vector。
### Stack ###
* Stack继承自Vector，实现一个**先进后出**的堆栈。
* Stack提供5额外的方法使得Vector得以被当做堆栈使用。
 * 基本的push和pop方法
 * peek方法得到栈顶的元素
 * empty方法测试堆栈是否为空
 * search方法检测一个元素在堆栈中的位置
* Stack刚创建后是空栈
## Set接口 ##
* 集(Set)是最简单的一种集合，它的对象不按特定方式排序，只是简单的把对象加入集合中，就像往口袋中放东西一样。
* 对集中成员的访问和操作是通过对象的引用进行的，**所以集中不能有重复的对象**
* 集也有多种变体，可以实现排序等功能，如TreeSet，它把对象添加到集中的操作将变为按照某种比较规则将其插入到有序的对象序列中
* Set接口继承Collection接口，每个具体的Set实现类依赖添加对象的**equals()**方法来检查独一性。Set接口没有引入新方法，所以Set就是一个Collection，只不过其行为不同。
### HashSet ###
* 使用HashMap的一个集的实现
* 虽然集定义成无序，但必须存在某种方法能相当高效地找到一个对象。使用一个HashMap对象实现集的存储和检索操作是在固定时间内实现的。
* 存放的对象个数有默认大小（16）
* Set中的元素是不能重复的，如果使用add(Object obj)方法添加已经存在的对象，则会**覆盖**前面的对象
### TreeSet ###
* TreeSet：在集中以升序对对象排序的集的实现。
* 这意味着从一个TreeSet对象获得第一个迭代器将按照升序提供对象。
## Map接口 ##
映射中存储的每个对象都有一个相关的关键字（Key）对象，关键字决定了对象在映射中的存储位置，检索对象时必须提供相应的关键字，就像在字典中查单词一样。**关键字应该是唯一的**。
### Hashtable ###
* Hashtable继承Map接口，实现一个 key-value 映射的哈希表。任何非空（non-null）的对象都可作为key或者value。
 * 添加数据使用put(key, value)
 * 取出数据使用get(key)  
这两个基本操作的事件开销为常数。
* Hashtable通过initial capacity和load factor两个参数调整性能。通常缺省的load factor **0.75**较好地实现了时间和空间的均衡。增大load factor可以节省空间但相应的查找时间将增大，这会影响像get和put这样的操作。
#### Hashtable基本方法 ####
* public synchronized void put(Object key,Object value)
 * 给对象value设定一关键字key,并将其加到Hashtable中。若此关键字已经存在，则将此关键字对应的旧对象更新为新的对象Value。这表明在哈希表中相同的关键字不可能对应不同的对象(从哈希表的基本思想来看，这也是显而易见的)
* public synchronized Object get(Object key)
 * 根据给定关键字key获取相对应的对象。
* public synchronized boolean containsKey(Object key)
 * 判断哈希表中是否包含关键字key
* public synchronized boolean contains(Object value)
 * 判断value是否是哈希表中的一个元素
* public synchronized object remove(object key)
 * 从哈希表中删除关键字key所对应的对象
* public synchronized void clear()
 * 清除哈希表
### HashMap ###
* HashMap和Hashtable类似 ,不存在同步性，但是允许使用Null键和Null值(除了非同步和允许使用 null 之外，HashMap 类与 Hashtable 大致相同)
* 同步性:Hashtable是线程安全的，也就是说是同步的，而HashMap是线程序不安全的，不是同步的 
## 排序 ##
* 结合集合类的对象实现Comparable
* 利用比较器，实现Comparator
### Comparable接口 ###
* java.lang包中，Comparable接口适合于一个类有自然顺序的时候。假定对象集合是同一个类型，该接口允许把集合排序成自然顺序

		int compartTo(Object o)
		比较当前实例对象与对象o，如果位于对象o之前，返回负值；如果两个对象在排序中的位置相同，则返回0；如果位于对象o后面，则返回正值
* 利用Comparable创建自己的排序规则，就是实现compareTo方法
### Comparator接口 ###
* 若一个类不能用于实现java.lang.Comparable,或者不喜欢缺省的Comparable行为，可以实现Comparator接口，定义一个新的比较器
		
		int compare(Obejct o1, Object o2)
		对两个对象o1和o2进行比较，如果o1位于o2的前面，则返回负值，如果在排序顺序中认为o1和o2是相同的，返回0，如果o1位于o2的后面，则返回正值

