# AWT #
* 图形用户界面(GUI)可以通过键盘或鼠标来响应用户的操作。
* 抽象窗口工具包(AWT)是一组Java类，此组Java类允许创建图形用户界面(GUI)。
* AWT提供用于创建生动而高效的GUI的各种组件。
## 相关名词 ##
* JFC是专门做图形界面用的类，一般主要指现在的Swing类，Java   API就是Java带的所有类和方法。
* java   API（java     Application   Programming   Interface）应该指的是所有的sun制定的应用程序接口，包括标准包和扩展包。       
* java   JFC(   Java   Foundation   Classes)   java基本类库，就是通常我们说的jdk，sdk中sun提供的类库       
* java类库就可以指   sun   提供的，第三方厂商（如IBM，bea等等）提供的，或者用户自己写的类库了。
## GUI ##
图形用户界面（Graphical User Interface，简称 GUI，又称图形用户接口）是指采用图形方式显示的计算机操作环境用户接口。与早期计算机使用的命令行界面相比，图形界面对于用户来说更为简便易用。
## AWT ##
抽象窗口工具包（Abstract Window Toolkit=AWT）是Java的平台独立的窗口系统， 图形和用户界面器件工具包。AWT是Java基础类（JFC）的一部分，为Java程序提供图形用户界面(GUI)的标准API。
### 容器 ###
* 可以存放组件的区域，可在容器上进行绘制和着色 
* java.awt包中的Container类可直接或间接派生出两个常用容器：框架（Frame类）和面板（Panel类）。
* 框架是一个带有边框的独立的窗口。
* 面板是包含在窗口中的一个不带边框的区域。
#### Container类 ####
* AWT使用Container类来定义最基本的构件容器,它有两个子类:Window类和Panel类.
在Window类还有两个子类
 1. 定义对话框,用Dialog子类;
Java还提了一个Dialog的子类---FileDialog, 用它生成文件对话框
 2. 定义一般意义的窗口,用Frame类.
#### Panel介绍 ####
* 使你更方便的组织你的构件,得到赏心悦目的布局
* Applet是Panel的子类,因此在小应用程序里可以直接加入构件,而一般的应用程序必须先定义构件容器.
* 小应用程序在浏览器中所显示的区域就是Panel,所占的尺寸就是缺省得Panel尺寸.
#### 框架 ####
* 框架是一个独立的窗口。
* 可以通过以下任一构造函数来创建：
 * Frame():创建一个不含标题的标准窗口
 * Frame(String Title): 创建一个含有标题的窗口，这个标题是由参数title指定的。
* 当一个Frame窗口被创建以后，需要调用setSize()方法来设置窗口的大小，并调用setVisible()来显示窗口。

		import java.awt.Event;
		import java.awt.Frame;
		public class MyAWT extends Frame{
		public static void main(String[] args) {
			Frame f = new MyAWT();
			f.setSize(200, 100);
			f.setVisible(true);
		}
		public boolean handleEvent(Event evt) {
			if(evt.id == Event.WINDOW_DESTROY)
				System.exit(0);
			else
				return super.handleEvent(evt);
			return true;
		}
		}

#### 面板 ####
* 面板不是一个单独的窗口，它只是包含在窗口中的一个区域。
* 面板是可以将许多组件组合起来的一种容器。
* 最简单的创建面板的方式就是通过面板的构造函数 Panel() 来进行。 
* 必须将面板添加到窗体中

		import java.awt.*;
	
		 class PanelTest extends Panel {
			public static void main(String args[]) {
		   	PanelTest p= new PanelTest();
			  	Frame f=new Frame("正在测试面板！");
			  	f.add(p);
			  	f.setSize(300,200);
			  	f.setVisible(true);
			}	
		 } 
### Layout的使用 ###
组件的放置需要考虑摆放位置
* Java一般不使用绝对定位，使用Layout进行定位
* Java常用的Layout分为
 * FlowLayout 
 * BorderLayout
 * GridLayout
#### FlowLayout ####
FlowLayout将组件从左到右排列，遇到放不下的时候就换行。
	
	import java.awt.Button;
	import java.awt.Event;
	import java.awt.FlowLayout;
	import java.awt.Frame;
	
	public class MyAWT extends Frame{
		public static void main(String[] args) {
			Frame f = new MyAWT();
			f.setLayout(new FlowLayout());
			f.setSize(640, 480);
			for(int i = 0; i < 20; i++)
				f.add(new Button("Button " + i));
			f.setVisible(true);
		}
		public boolean handleEvent(Event evt) {
			if(evt.id == Event.WINDOW_DESTROY)
				System.exit(0);
			else
				return super.handleEvent(evt);
			return true;
		}
	}  
#### BorderLayout ####
BorderLayout将组件按东南西北中来放置。放置时指定所放方位。

	import java.awt.BorderLayout;
	import java.awt.Button;
	import java.awt.Event;
	import java.awt.Frame;
	
	public class MyAWT extends Frame{
		public static void main(String[] args) {
			Frame f = new MyAWT();
			f.setSize(640, 480);
			f.setLayout(new BorderLayout());
			int i = 0;
			f.add("North", new Button("Button " + i++));
			f.add("South", new Button("Button " + i++));
			f.add("East", new Button("Button " + i++));
			f.add("West", new Button("Button " + i++));
			f.add("Center", new Button("Button " + i++));
			f.setVisible(true);
		}
		public boolean handleEvent(Event evt) {
			if(evt.id == Event.WINDOW_DESTROY)
				System.exit(0);
			else
				return super.handleEvent(evt);
			return true;
		}
	}
#### GridLayout ####
GridLayout将组件按格子放置

	import java.awt.Button;
	import java.awt.Event;
	import java.awt.Frame;
	import java.awt.GridLayout;
	public class MyAWT extends Frame{
		public static void main(String[] args) {
			Frame f = new MyAWT();
			f.setSize(640, 480);
			f.setLayout(new GridLayout(7,3));
			for(int i = 0; i < 20; i++)
				f.add(new Button("Button " + i));
			f.setVisible(true);
		}
		public boolean handleEvent(Event evt) {
			if(evt.id == Event.WINDOW_DESTROY)
				System.exit(0);
			else
				return super.handleEvent(evt);
			return true;
		}
	}
### Panel ###
Panel类(面板)
* 功能:容纳其他对象,安排合理布局
* 创建面板:

       Panel myPanel=new Panel();
       add(myPanel);
* 将面板作为容器:

    mypanel.add(button)


		import java.awt.*;
		public class Panel extends java.applet.Applet
		{    
			Panel panel1,panel2;
			Button button1,button2,button3,button4;
			public void init()
		  {  
				panel1=new Panel(); panel2=new Panel();
				add(panel1); add(panel2);
				button1=new Button("Button1");
				button2=new Button("Button2");
				button3=new Button("Button3");
				button4=new Button("Button4");
				panel1.add(button1);  panel1.add(button2);
				panel2.add(button3);  panel2.add(button4);
			}
		}
### AWT组件 ###
* 组件指可以放置在用户界面上的任何东西,可以将组件设置为可见或不可见,并在程序运行时可重新调整其大小。 
* AWT支持的组件：标签、文本域、文本区、按钮、复选框、选择框等。
* 高级组件包括滚动条、滚动窗格和对话框。
* 向窗口加入一个组件：首先生成所需组件的实例，然后调用add()方法，此方法是在Container类中定义的。
#### 标签 ####
可以通过以下任一构造函数来创建：

* Label( ) : 新建一个空标签
* Label(String labeltext): 新建一个包含给定文本的标签
* Label(String labeltext, int alignment):新建一个包含给定对齐方式的标签，对齐方式可以为 Label.LEFT、Label.RIGHT 或 Label.CENTER
#### 文本域 ####
可以通过以下任一构造函数来创建：

* TextField() : 新建一个文本域 
* TextField(int columns) : 新建一个包含给定列数的文本域 
* TextField(String s) : 新建一个包含给定字符串的文本域 
* TextField(String s, int columns) : 新建一个包含给定字符串和列数的文本域
#### 文本区 ####
可以通过以下构造函数来创建：

* TextArea( ) : 新建一个TextArea
* TextArea(int rows, int cols) : 新建一个包含给定行数和列数的TextArea
* TextArea(String text, int rows, int cols) : 新建一个包含给定字符串、行数和列数的TextArea
#### 按钮 ####
可以使用以下任一构造函数来创建按钮：

* Button() : 新建一个空的按钮
* Button(String text) : 新建一个包含给定字符串的按钮
#### 复选框 ####
可以使用以下任一构造函数来创建复选框：

- Checkbox()：创建一个空的复选框，且未被选中
- Checkbox(String text)：创建一个用给定字符串作为标签的复选框，且未被选中
- Checkbox(String text,Boolean on)：创建一个标签由参数text指定的复选框，允许通过参数on设定复选框的初始状态。

#### 单选按钮 ####
* 可以通过复选框组生成一系列互斥的复选框,实现单选按钮功能。 
* 在一组单选按钮中只能选择一个按钮。
* 首先创建一个 CheckboxGroup 对象。

 		CheckboxGroup cg=new CheckboxGroup();
* 然后再创建各单选按钮。  

	     Checkbox male=new Checkbox("男",cg,true);
	     Checkbox female=new Checkbox("女",cg,false);
#### 选择列表 ####
用 Choice 类可以创建一个选择框

	 Choice moviestars = new Choice( ); 
通过 addItem() 方法可以添加项目

	moviestars.addItem("安东尼奥.班德拉斯");
	moviestars.addItem("莱昂纳多.迪卡普尼奥");
	moviestars.addItem("桑德.布洛克");
	moviestars.addItem("休.葛兰特");
	moviestars.addItem("朱莉亚.罗萡茨"); 
#### Canvas ####
* 功能: 制作其他构件,通常用来放置图形图像,或绘图.
* 画图可以直接在applet区域上进行,定义了 Canvas对象后将paint()语句作为该对象的方法,这些动作就自动发生在画布区.
* 通常不需要处理画布上发生的事件
* 创建

	    Canvas canvas=new Canvas();
	    add(canvas);
### AWT中的事件 ###
和Applet一样，覆写`public boolean action(Event evt, Object arg)` 方法来进行事件处理

	import java.awt.Button;
	import java.awt.Event;
	import java.awt.FlowLayout;
	import java.awt.Frame;
	import javax.swing.JOptionPane;
	public class MyAWT extends Frame{
		Button b = new Button("test");
		public MyAWT() {
			this.setSize(100, 60);
			this.setLayout(new FlowLayout());
			this.add(b);
		}
		public boolean handleEvent(Event evt) {
			if(evt.id == Event.WINDOW_DESTROY) System.exit(0);
			else return super.handleEvent(evt);
			return true;
		}
		public boolean action(Event evt, Object arg) {
			if(evt.target.equals(b)) JOptionPane.showMessageDialog(null,"Hello"); 
			return true;
		}
		public static void main(String[] args) {
			Frame f = new MyAWT();
			f.setVisible(true);
		}
	}







 

