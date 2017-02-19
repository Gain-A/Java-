# 运行时类型判定 #
* RTTI(run-time type identification)的初期想法非常简单：当有一个指向基础型别base type的reference时，RTTI机制让你找出其所指的确切型别，不过当拓展到java.lang.reflection的时候，展现了全新的功能。即现在的Java中存在的两种形式的RTTI:
 * 传统的RTTI
 * reflection机制(反射机制)
## Class对象 ##
* 用来描述class的对象
* 程序中的每个class都有一个相应的Class对象。
	* 就是说你的新的class编译完成后，就会产生一个Class对象存储于相同的.class文件内。执行期间当你想要产生该class的对象时，JVM便会检查该类型的Class对象是否已经装载。如果尚未装载，JVM会根据名称找到.class文件并装载它。因此Java程序时并不会将整个程序都装载。
* 一旦某个性别的Class对象已经被装载，它就可以用来产生该性别的所有对象
* Class封装对象运行时的状态 
* 即使没有使用类创建对象，我们也可以实例化一个与该类相关的Class对象，`static Class forName(String className)`返回一个与参数className指定的类相关的Class对象
### Class 类创建的三种方式 ###
* 采用class字面常量
 * 类名.class  
	`eg:String.class int.class`
* 采用Class类的静态方法forName("test.Test")加载
 * 参数：包含完整包名.类名的字符串  
`Class.forName("java.lang.String");`
 * 对于内部类来说，可以用:  
`Class.forName("com.aowin.Outter$Inner");`

* 采用该类对象的getClass方法获得该类的类类型
<br>`Student stu = new Student();`<br>
`Class clazz = stu.getClass();`
    
* 三个Class引用指向同一个对象
    
    	Class c1 = String.class;
    	Class c2 = new String().getClass();
    	Class c3 = Class.forName("java.lang.String");
		c1 == c2; //true
		c2 == c3; //true
   
## 反射创建类对象 ##
1. 获取要创建类的类类型
2. Class对象调用newInstance()方法创建对象，要求该类中有空参数的构造方法
2. 获得构造器类Constructor类，可以采用类类型的getConstructor()方法，指定方法中的参数类型时，需要用到参数的类类型
 * 基本数据类型的类类型是`基本数据类型.class`，例如:`int.class`
3. 调用Constructor类的newInstance()方法，创建对象的实例,方法中的参数为**实际参数值**
 * 注意：私有权限的构造器在使用前，用setAccessable(true)取消权限检查
 	  
## 获取Class类对应类型的构造器 ##
* 获得public权限的构造器的方法
 * Class.getConstructors()
	   * 返回一个包含所有public构造器的Constructor[]
 * Class.getConstructor(Class<?>...parameterType)
		* 获得指定参数的public构造器对象
* 获得非public权限的构造器方法
 * 在Constructor对象调用newInstance()方法创建对象前，需要Constructor对象调用setAccessible(true)方法，否则会抛出`java.lang.IllegalAccessException`
 * Class.getDeclaredConstructors()
		* 返回一个包含所有构造器的Constructor[]
 * Class.getDeclaredConstructor(Class<?>...parameterType)
		* 获得指定参数的构造器对象

## 获取类的属性 ##
1. 获得分析的类的Class对象
2. 反射创建类的对象
3. 获取属性对象
4. 设置属性的值获取属性的值

### 获取属性对象 ###
* 获得public权限的属性
 * Class.getFields()
		* 包含所有public修饰的属性数组Field[]，包括继承而来的属性
 * Class.getField(String name)
		* 获得一个Field对象，它表示name指示的属性
* 获得非public权限的属性
 * Class.getDeclaredFields()
		* 返回表示该类声明的所有属性的Field[]
 * Class.getDeclaredField(String name)
		* 获得一个Field对象，它表示name指示的非public属性

### 获得属性的值 ###
* `get(Object obj)`	`返回Object`
 * 返回指定对象上此Field表示的字段的值
 * `getByte(Object obj)` `返回byte`
 * `getInt(Object obj)` `返回int`...等等方法 

### 设置属性的值 ###
* 在Field对象调用set方法给非public属性赋值前,要调用setAccessible(true)方法，否则会抛出`java.lang.IllegalAccessException`
* `set(Object obj, Object value)`
 * 将指定对象上的字段设置为指定值
 * `set(Object obj, boolean flag)`...等等方法

## 获得Class类类型对象类的方法 ##

* 获得所有public权限的方法
 * Class.getMethods()
		* 返回包含该类的所有public方法(包括继承来的)的Method[]
 * Class.getMethod(String name, Class<?>...parameterType)
		* 返回一个 Method 对象，它反映此 Class 对象所表示的类或接口的指定公共成员方法。
* 获得所有该类声明的方法(不包括继承而来的)
 * Class.getDeclaredMethods()
		* 返回 Method 对象的一个数组，这些对象反映此 Class 对象表示的类或接口声明的所有方法，包括公共、保护、默认（包）访问和私有方法，但不包括继承的方法。 
 * Class.getDeclaredMethod(String name, Class<?>...parameterType)
		* 返回Method对象，该对象表示名称为name，参数列表parameterTyped的方法

### Field对象调用方法 ###
* field.invole(Object obj, Object...args)
 * 其中obj表示哪个对象调用Field对象表示的那个方法，args表示参数列表的具体值
* 注意：在调用非public的方法前，需要调用Field对象的setAccessible(true)方法，取消权限检查，否则会抛出`java.lang.IllegalAccessException`

## 类型检查 ##
转型之间最好执行类型检查（避免运行期异常ClassCastException）
* 传统转型检查：**instanceof**  `if (obj instanceof Dog)`
 * 这种运算符是使用老式关键字，他要求obj必须为引用，所有不能用基本类型变量名，而后面的Dog也必须是Class，所以还是不能用基本类型。
 * 同时，有个缺点就是Dog本身必须是Class名，根本不能用某种变量替换，相比于下面的方法缺少灵活性
* 操作Class对象：
 * ClassObj.isInstance(obj)

		Class c = Dog.class;
		if( c.instanceOf(obj))...	//obj也要求是Object
