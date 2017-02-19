# Java介绍及JDK安装 #

1. 计算机概述（了解）

	    （1）计算机
	    （2）计算机硬件
		（3）计算机硬件
		       系统软件：Windows、Linux、Mac
			   应用软件：qq、yy
		（4）软件开发（理解）
		        软件：是由数据和指令组成的。（计算机）
				开发：就是把软件做出来。
				如何实现软件开发呢？
				    就是使用开发工具和计算机语言做出东西。
		（5）语言
	         自然语言：人与人交流沟通。
	         计算机语言：人与计算机交流沟通。
	            C、C++、C#、Java
	    （6）人机交互
				图形界面；操作方便直观
				DOS命令：需要记忆一些常见的命令
2. 键盘功能键的认识和快捷键（掌握）
	
	    （1）功能键的认识
				tab shift ctrl alt windows space 上下左右 enter 回车 截屏
		（2）快捷键
				Ctrl+C Ctrl+V Ctrl+X Ctrl+Z Ctrl+S Ctrl+A 
3. 常见的DOS命令（掌握）
	
		（1）常见的如下
				盘符的切换
					d:回车
				目录的进入
					cd android
					cd android\Java
				目录的回退
					cd ..
					cd \
				清除
					cls
				退出
					exit
		（2）其它的几个（了解）
				创建目录	md
				删除目录	rd
				创建文件	eco
				删除文件    del
				显示目录下的内容	dir	
				删除带内容的目录	rd aaa /s（询问）rd aaa /q（不询问）
			
4. Java语言概述（了解）
	
		（1）Java语言的发展史
				Java之父 詹姆斯.高斯林James.Gosling
				
				JDK1.4.2
				JDK5
				JDK7
		（2）Java语言的特点
				有很多小特点，重点有两个：开源、跨平台
		（3）Java语言是跨平台的，如何保证的呢？
				我们是通过翻译的案例讲解的：
				针对不同的操作系统，依靠不同的JVM来实现的。
		（4）Java语言的平台
				JavaSE
				JavaME  Android
				JavaEE
		
5. JDK、JRE、JVM的作用和关系（掌握）
	
		（1）作用
				JVM:保证Java语言跨平台
				JRE：Java程序的运行环境
				JDK：Java程序的开发环境
		（2）关系
				JDK：JRE+工具
				JRE：JVM+类库
6. JDK的下载，安装，卸载（掌握）
	
		（1）官网下载
		（2）安装
				A:绿色版  解压后直接使用
				B:安装版  需要安装后使用
				注意：
				安装目录最好不要带中文和空格
		（3）卸载
				A：绿色版  直接删除
				B：控制面板卸载
7. 第一个程序：HelloWorld案例（掌握）
	
		class HelloWorld {
			public static void main(String[] args) {
				System.out.println("HelloWorld");
			}
		}
		（1）程序解释：
				A:Java程序的最基本单位是类，所以我们要定义一个类
					格式：.class 类名
					举例：class HelloWorld
				B:在类中写内容的时候用大括号括起来
				C:Java程序想要执行，必须要main方法
					格式：public static void main (String[] args) 
				D:要指向哪些东西，也用大括号括起来
				E:你要做什么？今天我们仅仅做了一个简单的输出
					格式：System.out.println("HelloWorld");
					注意：""里面的东西是可以改动的
		（2）Java程序的开发执行流程
				A：编写Java源程序（.java）
				B：通过javac命令编译生成.class文件
				C:通过java命令运行.class文件
8. 常见的问题（掌握）
	
		（1）文件名被隐藏；
		（2）Java严格区分大小写；
		（3）Javac后加的是“文件名+拓展名”，Java后面加的是“文件名”，不加拓展名；
		（4）见到 “非法字符：\65307” 肯定是中英文字符问题；
		（5）括号的配对问题
9. 环境变量path（掌握）
	
		（1）path环境变量的作用
			保证javac命令可以再任意目录下运行，同理可以配置qq
		（2）path配置的两种方案
			方案1：（了解）
			方案2： 在系统变量里面找到环境变量
				    新建
						变量名：JAVA_HOME
						变量值：JDK安装文件下bin文件的目录
					修改
						变量名：path
						变量值：%JAVA_HOME%\bin;以前的内容
10. 环境变量classpath（掌握）
	
		（1）classpath环境变量的作用
				保证class文件可以在任意目录下运行
		（2）classpath环境变量的配置
				新建：
					变量名：classpath
					变量值：.class文件所在文件夹的地址