# Layout #
<hr>
## 容器、组件、布局和观感 ##
1. 容器和组件  
     组件是可以用图形化的方式显示在屏幕上并能够与用户进行交互的对象。
    容器是一种特殊的组件，一种能够容纳其他组件或容器的组件。
2. 布局管理器  
   为了使图形用户界面具有良好的平台无关性，提供了专门用来管理组件在容器中的布局的工具。
弄清楚容器、组件和布局管理器3者的关系。
3. 观感  
   决定swing应用程序的外观。
## 布局管理器 ##
Java中的布局类型包括以下几种：

* FlowLayout（流式布局）
* BorderLayout （边界布局） 
* GridLayout（网格布局）
* CardLayout （卡片布局） 
* BoxLayout (箱子布局)
* GridBagLayout（网格包布局）
### 布局管理器总体介绍 ###
* java.awt CardLayout 将组件象卡片一样放置在容器中，在某一时刻只有一个组件可见 
* java.awt FlowLayout 将组件按从左到右而后从上到下的顺序依次排列，一行不能放完则折到下一行继续放置 
* java.awt GridLayout 形似一个无框线的表格，每个单元格中放一个组件 
* java.awt BorderLayout 将组件按东、南、西、北、中五个区域放置，每个方向最多只能放置一个组件 
* java.awt GridBagLayout 非常灵活，可指定组件放置的具体位置及占用单元格数目 
* javax.swing BoxLayout 就像整齐放置的一行或者一列盒子，每个盒子中一个组件 
* Javax.swing SpringLayout 根据一组约束条件放置子组件
* Javax.swing ScrollPaneLayout 专用于JScrollPane，含一个Viewport，一个行头、一个列头、两个滚动条
### FlowLayout布局管理器 ###
* FlowLayout的构造函数有：
 * FlowLayout( ):生成一个默认的流式布局
 * FlowLayout(int alignment):可以设定每一行组件的对齐方式 
 * FlowLayout(int alignment,int horz,int vert):可以设定组件间的水平和垂直距离

* Applet和面板的缺省布局  
组件从左上角开始按从左到右、从上到下的方式排列  

		 FlowLayout mylayout = new FlowLayout();
		 FlowLayout exLayout = new FlowLayout(FlowLayout.RIGHT);
		 setLayout(exlayout); // 为容器设置新布局
### BorderLayout布局管理器 ###
* 下面是BorderLayout所定义的构造函数：

 -  BorderLayout( ):生成默认的边界布局
 - BorderLayout(int horz,int vert): 可以设定组件间的水平和垂直距离  
* 窗口、框架和对话框等的缺省布局,组件被置于容器的北、南、东、西或中间位置

		setLayout(new BorderLayout());
	    Button btnEast=new Button("东");
		Button btnWest=new Button("西");
		Button btnNorth=new Button("北");
		Button btnSouth=new Button("南");
		Button btnCenter=new Button("中");
		add(btnEast,BorderLayout.EAST);
		add(btnWest,BorderLayout.WEST);
		add(btnNorth,BorderLayout.NORTH);
		add(btnSouth,BorderLayout.SOUTH);
		add(btnCenter,BorderLayout.CENTER)
### GridLayout布局管理器 ###
* GridLayout的构造函数如下所示：

  * GridLayout():生成一个单列的网格布局
  * GridLayout(int row,int col):生成一个设定行数和列数的网格布局
  * GridLayout(int row,int col,int horz,int vert)：可以设置组件之间的水平和垂直间隔
* 用于将容器区域划分为一个矩形网格,组件按行和列排列

		Button btn[]; // 声明按钮数组
		String str[]={"1","2","3","4","5","6","7","8","9"};
		setLayout(new GridLayout(3,3));
		btn=new Button[str.length]; // 创建按钮数组
		for(int i=0;i<str.length;i++){
			btn[i]=new Button(str[i]);  add(btn[i]);
		}
### CardLayout布局管理器 ###
* 可存储几个不同的布局。
* 每个布局就像是一个卡片组中的一张卡片。
* 在一个给定的时间总会有一张卡片在顶层。
* 卡片通常为一个 Panel 对象。 
* 每当需要许多面板切换，而每个面板需要显示为不同布局时，可以使用卡片布局
### BoxLayout布局管理器 ###
按照从上到下（即Y轴）或者从左到右（即X轴）的顺序来依次排列组件
### ScrollPaneLayout布局管理器 ###
是JScrollPane中的内置布局管理器，所以不需要单独创建，会自动设置
### Null布局管理器 ###
* 在某些情况下，用户不想使用布局管理器，需要自己设置组件的位置和大小，这时应取消容器的布局管理器，然后再进行设置，否则用户自定义设置将会被布局管理器覆盖。取消布局管理器的方法是：  
 `setLayout(null);`  
用户使用setLocation()、setSize()、setBounds()等方法为组件设置位置和大小。需要注意的是，这种方法会导致程序与系统相关，如不同的分辨率会产生不同的效果。
### GridBagLayout布局管理器 ### 
* 通过使用以下语法容器可获得 GridBagLayout：

		GridBagLayout gb=new GridBagLayout();
		ContainerName.setLayout(gb);
* 要使用此布局，必须提供各组件的大小和布局等信息。
* GridBagConstraints 类中包含 GridBagLayout 类用来定位及调整组件大小所需的全部信息。  
  组件大小不必相同  
  组件按行和列排列  
  放置顺序不一定为从左至右和由上至下
  
# 事件 #
* 事件－用户对组件的一个操作，称之为一个事件，是一个描述发生了什么的对象
* 事件源－事件的产生器（发生事件的组件）
* 事件处理器－接收事件、解释事件并处理用户交互的方法。
* 弄清楚事件、事件源和事件处理器三者的关系
## 事件源 ##
* 事件源是一个事件的产生者。例如，在Button组件上点击鼠标会产生以这个Button 为源的一个ActionEvent.  这个ActionEvent实例是一个对象，它包含关于刚才所发生的那个事件的信息的对象。这些信息包括：

		getActionCommand－返回与动作相关联的命令名称。
		GetModifiers－返回在执行动作时持有的修饰符
## 事件处理器 ##
* 事件处理器就是一个接收事件、解释事件并处理用户交互的方法。 
* Java程序对事件进行处理的方法是放在一个类对象中的，这个类对象就是事件监听器。
* 我们必须将一个事件监听器对象同某个事件源的某种事件进行关联，这样，当某个事件源上发生了某种事件后，关联的事件监听器中的有关代码才会被执行。我们把这个关联的过程称为向事件源注册事件监听器对象。
* 事件处理器首先与组件（事件源）建立关联，当组件接受外部作用（事件）时，组件就会产生一个相应的事件对象，并把此对象传给与之关联的事件处理器，事件处理器就会被启动并执行相关的代码来处理该事件。
## JDK 1.0层次模型的特点 ##
* 优点 
 * 简单，而且非常适合面向对象的编程环境。
* 缺点
 * 事件只能由产生这个事件的组件或包含这个组件的容器处理。
 * 为了处理事件，你必须定义接收这个事件的组件的子类，或者在基容器创建handleEvent()方法。
## JDK 1.1委托事件模型 ##
* 委托事件模型是在JDK1.1中引入的。在这个模型中，事件被送往产生这个事件的组件，然而，注册一个或多个称为监听者的类取决于每一个组件，这些类包含事件处理器，用来接收和处理这个事件。采用这种方法，事件处理器可以安排在与源组件分离的对象中。监听者就是实现了Listener接口的类。
* 事件是只向注册的监听者报告的对象。每个事件都有一个对应的监听者接口，规定哪些方法必须在适合接收那种类型的事件的类中定义。实现了定义那些方法的接口的类可以注册为一个监听者。 
* 从没有注册的监听者的组件中发出的事件不会被传播 
* 有可能创建并使用适配器(adapter)类对事件动作进行分类。
* 委托模型有利于把工作分布到各个类中。
* 新的事件模型提供对JavaBeans的支持。
## 事件类型 ##
* 我们已经介绍了在单一类型事件上下文中从组件接收事件的通用机制。事件类的层次结构图如下所示。许多事件类在java.awt.event包中，也有一些事件类在API的其他地方。
* 对于每类事件，都有一个接口，这个接口必须由想接收这个事件的类的对象实现。这个接口还要求定义一个或多个方法。当发生特定的事件时，就会调用这些方法 
## 事件处理模型 ##
* Java 最新的事件处理方法是基于授权事件模型
* 当事件来源对象因用户的操作（鼠标或键盘），系统会自动触发此事件类对象E，并通知所授权的事件监听者A（若来源对象已向A注册），事件监听者A中有处理各种事件的方法(事件处理者1~n)便会处理此事件E的各种状况 。

|事件类|说明|事件源|
|::|::|
|ActionEvent|通常按下按钮，双击列表项或选中一个菜单项时，就会生成此事件|Button、List、MenuItem、TextField|
|AdjustmentEvent |操纵滚动条时会生成此事件|Scrollbar|
|ComponentEvent |当一个组件移动、隐藏、调整大小或成为可见时会生成此事件|Component|
|ItemEvent |单击复选框或列表项时，或者当一个选择框或一个可选菜单的项被选择或取消时生成此事件|Checkbox、CheckboxMenuItem、Choice、List|
|FocusEvent |组件获得或失去键盘焦点时会生成此事件|Component|
|KeyEvent |接收到键盘输入时会生成此事件|Component |
|MouseEvent |拖动、移动、单击、按下或释放鼠标或在鼠标进入或退出一个组件时，会生成此事件|Component|
|ContainerEvent |将组件添加至容器或从中删除时会生成此事件|Container|
|TextEvent  |在文本区或文本域的文本改变时会生成此事件|TextField、TextArea|
|WindowEvent |当一个窗口激活、关闭、失效、恢复、最小化、打开或退出时会生成此事件|Window|
### 事件方法类型和接口 ###
|Category|Interface Name|Methods|
|::|::|::|
|Action|ActionListener|actionPerformed(ActionEvent)|
|Item|ItemListener|itemStateChanged(ItemEvent)|
| Mouse  motion|MouseMotionListener|mouseDragged(MouseEvent)、mouseMoved(MouseEvent)|
|Mouse  button|MouseListener|mousePressed(MouseEvent)、mouseReleased(MouseEvent)、mouseEntered(MouseEvent)、mouseExited(MouseEvent)、mouseClicked(MouseEvent)|
|Key|KeyListener |keyPressed(KeyEvent)、keyReleased(KeyEvent)、keyTyped(KeyEvent)|
|Focus|FocusListener |focusGained(FocusEvent)、focusLost(FocusEvent)|
|Adjustment|AdjustmentListener |adjustmentValueChanged 
(AdjustmentEvent)|
|Component|ComponentListener |componentMoved(ComponentEvent)、componentHidden(ComponentEvent)、componentResized(ComponentEvent)、componentShown(ComponentEvent)|
### 多监听者 ###
* AWT事件监听框架事实上允许同一个组件带有多个监听者。一般地，如果你想写一个程序，它基于一个事件而执行多个动作，把那些行为编写到处理器的方法里即可。然而，有时一个程序的设计要求同一程序的多个不相关的部分对于同一事件作出反应。这种情况是有可能的，例如，将一个上下文敏感的帮助系统加到一个已存在的程序中。
* 监听者机制允许你调用addXXXlistener方法任意多次，而且，你可以根据你的设计需要指定任意多个不同的监听者。事件发生时，所有被注册的监听者的处理器都会被调用。 
### 事件Adapters(适配器)  ###
* 你定义的Listener可以继承Adapter类，而且只需重写你所需要的方法。例如：

实现每个Listener接口的所有方法的工作量是非常大的，尤其是MouseListener接口和ComponentListener接口。  
以MouseListener接口为例，它定义了如下方法：

	mouseClicked(MouseEvent)
	mouseEntered(MouseEvent)
	mouseExited(MouseEvent)
	mousePressed(MouseEvent)
	mouseReleased(MouseEvent)
为了方便起见，Java语言提供了Adapters类，用来实现含有多个方法的类。这些Adapters类中的方法是空的。
你可以继承Adapters类，而且只需重写你所需要的方法。例如：
	
	   import java.awt.*;
	   import java.awt.event.*; 
	   
	   public class MouseClickHandler extends MouseAdapter { 
	   
	   // We just need the mouseClick handler, so we use 
	   // the Adapter to avoid having to write all the 
	   // event handler methods 
	   public void mouseClicked (MouseEvent e) { 
	  // Do something with the mouse click... 
	  } 
	} 
### 匿名类 ###
可以在一个表达式的域中，包含整个类的定义。这种方法定义了一个所谓的匿名类并且立即创建了实例。匿名类通常和AWT事件处理一起使用。 




 

