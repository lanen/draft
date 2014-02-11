
JDBC 访问数据库
==============


# 使用JDBC 访问数据库方式
	

<pre>

	public void connectToAndQueryDatabase(String username, String password) {
		
		//加载驱动,建立连接
	    Connection con = DriverManager.getConnection(
	                         "jdbc:myDriver:myDatabase",
	                         username,
	                         password);
		
		//查询 Statement 
	    Statement stmt = con.createStatement();
	    ResultSet rs = stmt.executeQuery("SELECT a, b, c FROM Table1");
		
		//获取结果集
	    while (rs.next()) {
	        int x = rs.getInt("a");
	        String s = rs.getString("b");
	        float f = rs.getFloat("c");
	    }
	}

</pre>

# DataSource

J2SE 只定义了java.sql.DataSource 接口,可以在c3p0,proxool 等连接池产品中获取实现。


	<dependency>
		<groupId>c3p0</groupId>
		<artifactId>c3p0</artifactId>
		<version>0.9.1.2</version>
	</dependency>
            
	<dependency>
		<groupId>com.cloudhopper.proxool</groupId>
		<artifactId>proxool</artifactId>
		<version>0.9.1</version>
	</dependency>
            

	<dependency>
		<groupId>com.alibaba</groupId>
		<artifactId>druid</artifactId>
		<version>1.0.2</version>
	</dependency>
            


# JdbcTemplate


# 使用alibaba 的druid 连接池管理方案



http://blog.csdn.net/blogdevteam/article/details/7750513





