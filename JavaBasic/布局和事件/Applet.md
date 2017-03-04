# Applet #
<hr>
## 什么是Applet ##
Java Applet 是用Java 语言编写的一些小应用程序，这些程序是直接嵌入到页面中，由支持Java的浏览器(IE 或 Nescape)解释执行能够产生特殊效果的程序。它可以大大提高Web页面的交互能力和动态执行能力。包含Applet的网页被称为Java-powered页，可以称其为Java支持的网页。 

当用户访问这样的网页时，Applet被下载到用户的计算机上执行，但前提是用户使用的是支持Java的网络浏览器。由于Applet是在用户的计算机上执行的，所以它的执行速度不受网络带宽或者Modem存取速度的限制，用户可以更好地欣赏网页上Applet产生的多媒体效果。 

Applet 小应用程序的实现主要依靠**java.applet 包中的Applet类**。与一般的应用程序不同，Applet应用程序必须嵌入在HTML页面中，才能得到解释执行；同时Applet可以从Web页面中获得参数，并和Web页面进行交互。 

## 开发步骤 ##
* 建立Java Applet源程序
* 把Applet的源程序转换为字节码文件 
* 编制使用class 的HTML文件。在HTML文件内放入必要的<APPLET>语句
## 一个简单的Applet ##
	import java.awt.*;
	import java.applet.*;
	public class MyApplet extends Applet //继承Appelet类，这是Appelet Java程序的特点 {
		public void paint(Graphics g ) {　　g.drawString("Hello World!",5,35);
		}
	} 


## 查看运行结果 ##
* 使用AppletViewer查看
* 在网页中查看

		<HTML>
		<TITLE>HelloWorld! Applet</TITLE>
		<APPLET	CODE=" MyApplet.class" WIDTH=200 HEIGHT=100>
		</APPLET>
		</HTML>

## Applet方法 ##
* init() --程序片第一次被创建，初次运行初始化程序片时调用
* start() --每当程序片进入Web 浏览器中，并且允许程序片启动它的常规操作时调用，并且是在init()后调用
* stop()-- 每次程序片从Web 浏览器的视线中离开时调用，使程序片能关闭代价高昂的操作，并且是在调用destroy()前调用
* destroy()-- 程序片不再需要，将它从页面中卸载时调用，以执行资源的最后清除工作
* paint() 基础类Component 的一部分（继承结构中上溯三级）。作为update() 的一部分调用，以便对程序片的画布进行特殊的描绘

### paint()方法 ###
* Applet本身是一个容器,因此任何输出都必须用图形方法paint()
* 当小应用首次被装载，以及每次窗口放大、缩小、刷新时都要调用paint方法
* paint()是由浏览器调用的, 而不是由程序调用，当程序希望调用paint方法时，用repaint命令
* paint方法的参数是Graphics类的对象 g，它在java.awt.Graphics内
## Applet组件 ##
* Button	按钮
* TextField	文本框
* TextArea	文本区域
* Label		标签
* CheckBox	复选框
* RadioButton	单选框
* DropDown List	下拉列表
* List		列表
### 含有组件的applet ###
	//:Button1.java 
	import java.awt.*; 
	import java.applet.*; 
	public class Button1 extends Applet { 
		Button b1 = new Button("Button 1"); 
		Button b2 = new Button("Button 2"); 
		public void init() { 
			add(b1); 
			add(b2); 
		} 
	} // <applet code=Button1.class width=200 height=70></applet>
### Applet中的事件 ###
	//: Button2.java 
	import java.awt.*; 
	import java.applet.*; 
	public class Button2 extends Applet { 
		Button b1 = new Button("Button 1"); 
		Button b2 = new Button("Button 2"); 
		public void init() { 
			add(b1); 
			add(b2); 
		} 
		public boolean action(Event evt, Object arg) { 
			if ( evt.target.equals(b1) ) {
				showStatus("Button 1"); 
			} else if ( evt.target.equals(b2) ) {
				showStatus("Button 2"); 
			} else {
				return super.action(evt,arg); 
			}
			return true; 
		} 
	} // <applet code=Button2.class width=200 height=70></applet>
	





 

