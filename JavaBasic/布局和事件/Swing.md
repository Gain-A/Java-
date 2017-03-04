# Swing #
* SUN的AWT：Java处理图形用户界面的初始途径。AWT库处理图形的基本方法：把这些元素的创建和行为交给目标平台上的本地GUI工具箱进行处理。
* 理论上 “一次编写，随处运行”。
* 实际上“一次编写，随处调试”。
* Sun与Netscape合作开发出：Swing。
## Swing和AWT的关系 ##
* AWT为每一个组件分配一个操作系统窗口。大型应用程序中，大量这样的窗口会占用大量资源降低系统性能。
* Swing的很多用户界面元素，如菜单、按钮等，都是画在他们的容器中的。占用更少的系统资源，增加了更多的组件，且允许控制程序的外观。
* Swing并不是完全摒弃AWT，而是一组建立在AWT之上的包，它提供了大量预建的类，

		import java.awt.*;
		import javax.swing.*;
## Swing介绍 ##
* 可插的外观和感觉
 * 应用程序看上去是与平台有关的
 * 有客户化的Swing组件

* Swing的体系结构
 * 它是围绕着实现AWT各个部分的API构筑的
 * 大多数组件不象AWT那样使用与平台相关的实现
* Swing提供了一整套GUI组件，为了保证可移植性，它是完全用Java语言编写的
### 可插的外观和感觉 ###
可插的外观和感觉使得开发人员可以构建这样的应用程序：它们可以在任何平台上执行，而且看上去就象是专门为那个特定的平台而开发的。一个在Windows环境中执行的程序，似乎是专为这个环境而开发的；而同样的程序在Unix平台上执行，它的行为又似乎是专为Unix环境开发的。

开发人员可以创建自己的客户化Swing组件，带有他们想设计出的任何外观和感觉。这增加了用于跨平台应用程序和Applet的可靠性和一致性。一个完整应用程序的GUI可以在运行时刻从一种外观和感觉切换到另一种 
## Swing的体系结构  ##
与AWT比较，Swing提供了更完整的组件，引入了许多新的特性和能力。Swing API是围绕着实现AWT各个部分的API构筑的。这保证了所有早期的AWT组件仍然可以使用。AWT采用了与特定平台相关的实现，而绝大多数Swing组件却不是这样做的，因此Swing的外观和感觉是可客户化和可插的。 

### JFrame ###
* 在Java的GUI程序中，需要一个框架窗口(JFrame)来放置其它的层板和组件。
* JFrame的默认大小为0×0并且是不可见的，用setBounds方法设置框架的大小，setVisible(true)显示窗口
* 框架是一个容器
* 组件添加在内容窗口上
* 是放置其他 Swing 组件的顶级容器
* JFrame 组件用于在 Swing 程序中创建窗体
* 它的构造函数：

	    JFrame()
	    JFrame(String Title)
* 组件必须添加至内容窗格，而不是直接添加至 JFrame 对象，示例：

           	 frame.getContentPane().add(b);
### JPanel ###
* JPanel 组件是一个中间容器
* 用于将小型的轻量级组件组合在一起
* JPanel 的缺省布局为 FlowLayout
* JPanel 具有下列构造函数：

		JPanel()
		JPanel(LayoutManager lm)
### JLabel ###
* 它既可以显示文本也可以显示图像
* 构造函数如下：

		JLabel（String str） 文本内容
		JLabel(Icon icon)：icon表示使用的图标
		JLabel(String text,Icon icon,int align)：text表示使用的字符串; icon表示使用的图标;align表示水平对齐方式，其值可以为：LEFT、RIGHT、CENTER。
* 其它常用方法

   		getText()
       	setText(String text)
### JButton ###
* 可以使用以下任一构造函数来创建按钮：

	JButton() : 新建一个空的按钮
	JButton(Icon icon)
	JButton(String text)
	JButton(String text, Icon icon)
### JTextField ###
* JTextField 组件允许输入或编辑单行文本
* 此类的构造函数包括：

		JTextField()
		JTextField(Document doc, String text, int columns)
		JTextField(int columns)
		JTextField(String text)
		JTextField(String text, int columns)
### JPasswordField ###
* JPasswordField 组件允许输入或编辑单行文本，并且文本被其他字符代替。
* 此类的构造函数与单行文本框类似。
* 其它方法：

		char[] getPassword()
		char getEchoChar()
		void setEchoChar(char c)
### JTextArea ###
* JTextArea 组件用于接受来自用户的多行文本它可实现可滚动界面
* JTextArea 组件可使用下列构造函数创建：

		JTextArea()
		JTextArea(int rows, int cols)
		JTextArea(String text)
### JCheckBox ###
* 复选框用于为用户提供一组选项
* JCheckBox 类具有下列构造函数：

		JCheckBox()
		JCheckBox(Icon icon)
		JCheckBox(Icon icon, boolean selected)
		JCheckBox(String text)
		JCheckBox(String text, boolean selected)
		JCheckBox(String text, Icon icon)
		JCheckBox(String text, Icon icon, boolean selected)
### JRadioButton ###
* 单选按钮允许用户从多个选项中选择其中一个
* ButtonGroup 用于在 Swing 中创建组
* JRadioButton 对象可使用下列构造函数创建：

		JRadioButton()
		JRadioButton(Icon icon)
		JRadioButton(Icon, boolean selected)
		JRadioButton(String text)
		JRadioButton(String text, boolean selected)
		JRadioButton(String text, Icon icon)
		JRadioButton(String text, Icon icon, boolean selected)
### JList（列表框） ###
* JList会在屏幕上持续占用固定行数的空间。如果你想选取列表内的项目，只要调用getSelectedValues（）就可以得到一个string数组。
* public JList() : 使用空模型构造 JList
* public JList(ListModel dataModel) :构造一个列表，用它显示指定模型中的元素。 
* public JList (Object [] listData) :构造一个列表以显示指定数组listData的元素。 
* JList 不支持滚动。要启用滚动，可使用下列代码:

		   JScrollPane myScrollPane=new JScrollPane();
			myScrollPane.getViewport().setView(dataList);
### JComboBox ###
* 文本域和下拉列表的组合
* 在 Swing 中，组合框由 JComboBox 表示
* 构造函数如下：
		
		public JComboBox() : 此构造函数使用缺省数据模型创建 JComboBox
		public JComboBox(ComboBoxModel asModel) : 使用现有 ComboBoxModel 中的项目的组合框
		public JComboBox(Object [] items) : 包含指定数
### JMenu ###
* 菜单显示项目列表，指明各种任务。
* 选择或单击某个选项时会打开另一个列表或子菜单。
* Swing 菜单由菜单栏、菜单和菜单项构成。
* 菜单栏是所有菜单和菜单项的根
### 菜单 ###
* JMenuBar 是可通过 JFrame、JWindow 的根窗格添加至容器的组件。
* 由多个 JMenu 组成，每个 JMenu 在 JMenubar 中都表示为字符串。
* JMenu 在 JMenuBar 下以文本字符串形式显示，而在用户单击它时，则以弹出式菜单显示。
* JMenuItem为JMenu 中的一个组件，以文本字符串形式显示，可以具有图标，外观可以修改，如字体、颜色、背景、边框等。
### 对话框 ###
* JOptionPane对话框   
  是模式对话框，它提供了很多现成的对话框样式，可以供用户直接使用。 
* JFileChooser对话框   
  提供了标准的文件的打开、保存对话框。
### JTable ###
	JFrame frame = new JFrame();
	Object[][] data = { { "1", "2", "3" }, { "a", "b", "c" } };
	Object[] name = { "age", "name", "sex", "gride" };
	
	// 设计table模板
	DefaultTableModel model = new DefaultTableModel(data, name);
	// 利用模板生成table
	JTable table = new JTable(model);
	// 把table加到jscollpanel
	JScrollPane scollPanel = new JScrollPane(table);



