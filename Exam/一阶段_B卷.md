# 第一阶段B卷 #
1. 编译和运行以下代码，将会得到什么结果？( )

		public classThrowsDemo{
			static void throwMethod(){
				System.out.println("Inside throwMethod");
				throw new IllegalAccessException("Demo");
			}
			
			public static void main(String[] args){
				try{
					throwMethod();
				} catch(IllegalAccessException e) {
					System.out.println("Caught" + e);
				}
			}
		}

		A、 编译时发生错误
		B、 运行时发生错误
		C、 编译成功，但是没有任何输出
		D、 输出结果为：
		Inside throwMethod. followed by Caught: java.lang.IllegalAccessException:demo
2. 以下哪些说法是正确的？( )

		A、 静态方法不能访问隐含变量this
		B、 静态方法不需要建立一个类的实例就可以直接访问
		C、 final声明的方法不能被继承
		D、 静态方法不能继承
3. 以下哪些说法是正确的？()

		CREATE TABLE`student`(
			`id` int(12) NOT NULL,
			`name` varchar(22) default 'tom',
			`age` int(12) default NULL,
			`sex` varchar(12) default NULL,
			PRIMARY KEY (`id`)
		) ENGINE=InnoDB DEFAULT CHARSET=gb2312;


		import com.mysql.jdbc.*;
		import java.sql.DriverManager;
		import java.sql.ResultSet;
		
		public class Base_flow{
			 String driver = "com.mysql.jdbc.Driver";
			 String url = "jdbc:myal://localhost:3306/mydatabase?useUnicode=true&characterEncoding=gb2312";
			 String user = "root";
			 String psd = "mysql";
			 Connection conn = null;
			 Statement st = null;
			 ResultSet rs = null;
			 String sql = null;
			 try{
				 Class.forName(driver);
				 //下行为第1处
				 st = DriverManager.getConnection(url, user, psd).createStatement();
				 sql = "select * from student";
				 //下行为第2处
				 rs = st.execute(sql);
				 while(rs.next()){
					 //下行为第3处
					 System.out.println(rs.getString("id"));
					 System.out.println(rs.getString("name"));
					 System.out.println(rs.getInt("age"));
					 System.out.println(rs.getString("class"));
				 } catch (SQLException e){
					 System.out.println("操作过程中失败");
				 } catch(ClassNotFountdException e){
					 e.printStackTrace();
				 } finally{
					 try{  //try语句块中为第4处
						 if(st != null)
							 	st.close();
						 if(rs != null)
							 	rs.close();
						 if(conn != null)
							 	conn.close();
					 } catch (SQLException e){
						 System.out.println("关闭失败");
					 }
				 }
			 }
		 }

		A、 1处编译异常
		B、 2处编译异常
		C、 3处，如果数据库声明为ID，则运行异常
		D、 4处的try代码块编译期异常
4. 根据以下层次和代码片段：
  
		java.lang.Throwable
			java.lang.Error
				java.lang.OutOfMemoryError
					java.io.StreamCorruptedException
			java.lang.Exception
				java.io.IOException
					java.net.MalformedURLException
		
		try{
			URL u = new URL(s);//assume s is previously defined
			Object o = in.readObject();//in is an ObjectInputStream
			System.out.println("Success");
		} catch(MalformedURLException e){
			System.out.println("Bad URL");
		} catch(StreamCorruptedException e){
			System.out.println("Bad file contents");
		} catch(Exception e){
			System.out.println("General Exception");
		} finally{
			System.out.println("Doint finally part");
		} 
		
		System.out.println("Carrying on");
如果第4行抛出一个OutOfMemoryError错误，以下哪一行以及以上的catch或者finally语句块中的语句不会执行？()  

		A、 9		B、 13		C、 17 		D、 21		E、 23
5. 根据下面的类层次关系图：  

		Animal 
			Mammal
				Dog
				Cat (implements Washer)
				Raccoon (implements Washer)
				SwampThing	
有以下代码:  

		1. Cat sunFlower;
		2. Washer wawa;
		3. SwampThing pogo;
		4. 
		5. sunflower = new Cat();
		6. wawa = sunflower;
		7. pogo = (SwapThing)wawa;
哪些选项的描述是正确的？()  

		A、 Line 6 will not compile; an explicit cast is required to convert a Cat to a Washer.
		B、 Line 7 will not compile,because you cannot cast an interface to a class
		C、 The code will compile and run, but the cast in line 7 is not required and can be eliminated 
		D、 The code will compile but will throw an exception at line 7, because runtime conversion from an interface to a class is not perimtted
		E、 The code will compile but will throw an exception at line 7, because runtime class of wawa cannot be convert to type SwampThing
6. Java的监听器要么就是继承了Thread类，要么就是实现了Runnable接口 True/False?()
	
	A、 True 		B、 False








答案：


		1. A
		2. A、B
		3. A、B
		4. C
		5. E
		6. B






