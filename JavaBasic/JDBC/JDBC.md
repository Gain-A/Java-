# JDBC #
* Java Database Connectivity
* JDBC提供了Java连接数据库服务器的支持
## JDBC架构 ##
* JDBC API
 * 由工程师写好，共程序员调用的接口和类
* JDBC DriverManager
 * JDBC Driver的管理器
* JDBC Driver
 * 负责连接到不同的数据库
## JDBC编程步骤 ##
1. Load the Driver(加载数据库驱动器)
 * Class.forName(“com.mysql.jdbc.Driver”);
 * Class.forName(“oracle.jdbc.driver.OracleDriver”);
2. Connect to the Database(连接到数据库)
 * Connection conn=DriverManager.getConnection(strURL, strUser,strPass);
3. Execute the SQL(执行SQL语句)

 		Statement stmt = conn.createStatement();
		stmt.executeQuery(sql);	//select
		stmt.executeUpdate(sql); //update,delete,insert
4. 取得结果

		ResultSet rs = stmt.executeQuery("select * from user");
		while(rs.next()){
			System.out.println(rs.getInt("id") + "\t" + rs.getString("name"));
		}
5. Close
 * Close ResultSet
 * Close Statement
 * Close Connection
## 四大物件 ##
* DriverManager: 根据数据库的不同，调用正確的 Driver
* Connection:由 Driver 产生,连接数据库,负责和数据库的连接,进行信息的传输
* Statement : 由 Connection 产生,负责传送 SQL 指令到服务器
* ResultSet : 负责接受Statememt(Sql 指令)执行后的结果
### DriverManager ###
* 提供程序员调用 JDBC Driver时统一的接口
* 免除程序员针对不同数据库编写不同代码的困扰
### Statement ###
定义:把sql发送到数据库服务器的类,有三种

* Statement
 * 一般的 Statement 
 * SQL发送到数据库服务器先经过编译再执行
* PreparedStatement
 * 将SQL语句内某些值暂时放空(用?代替)，待执行的时候再为？赋值的Statement
 * SQL 语句第一次发送到数据库服务器需编译，资料库会把编译后的 SQL 语句暂存在缓存里面，稍后调用时即可直接執行，不需编译。适合在循环中调用
* CallableStatement
 * 调用服务器的 Stored Procedure 的Statement 物件
 * 所有 Stored Procedure 都事先经过编译，直接调用即可。Stored Procedure 适合做为 “代码和数据库分离” 之用
#### 如何产生Statement ####
* 由 Connection.createStatement() 生成;

		String strSQL = "SELECT * FROM accounts";
		Statement stmt= conn.createStatement();
		stmt.executeQuery(strSQL);
### PreparedStatement ###
* 带参数的 SQL 指令
* 第一次被执行时先被编译，然后缓存在内存中等待被调用
* 适用与有参数变化，或放在循环中执行的场合
	
		mport java.sql.*;
		...
		String strSQL = "SELECT * FROM CUSTOMERS WHERE custCompany = ?";
		PreparedStatement prepStmt = conn.prepareStatement(strSQL);
		prepStmt.setString(1, "ABC Tech Inc.");
		...
		ResultSet rs = prepStmt.executeQuery();
* 它是一個继承 Statement 类的接口
 * public interface PreparedStatement extends Statement
#### 批处理 ####
* 采用Statement实现

		Connection conn =null;
		Statement stmt =null;
		ResultSet rs =null;
		Class.forName("com.mysql.jdbc.Driver"); //获得数据库驱动
		conn= DriverManager.getConnection("jdbc:mysql://localhost:3306/Class","root",“mysql");
		
		stmt=conn.createStatement();
		stmt.addBatch("insert into user values(200,'ccc')");
		stmt.addBatch("insert into user values(201,'ddd')");
		    
		stmt.executeBatch();
		    
		stmt.close();
		conn.close();
* 采用PreparedStatement

		Connection conn =null;
		PreparedStatement stmt =null;
		Class.forName("com.mysql.jdbc.Driver"); //获得数据库驱动
		conn= DriverManager.getConnection("jdbc:mysql://localhost:3306/Class","root",“mysql");
		
		stmt=conn.prepareStatement("insert into user values(?,?)");
		stmt.setInt(1, 100);
		stmt.setString(2, "aaa");
		stmt.addBatch();
		    
		 stmt.setInt(1, 101);
		 stmt.setString(2, "bbb");
		 stmt.addBatch();    
		 stmt.executeBatch();
		    
		stmt.close();
		conn.close();
## 事务Transaction ##
例如，转账的例子。

	实现:
	Try{
	Conn.setAutoCommit(false);
	执行sql语句1;
	执行sql语句2;
	….
	Conn.commit();
	Conn.setAutoCommit(true);
	}catch(Exception e)
	{
	Conn.rollback();
	Conn.setAutoCommit(true);
	}
	默认情况下为true,即自动提交;
	Conn.setAutoCommit(true);
## 中文处理 ##
	jdbc:mysql://localhost:3306/class?useUnicode=true&characterEncoding=utf8



 
 

