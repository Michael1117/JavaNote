## JDBC

#### JDBC：

​	1.概念： Java DataBase Connectivity       Java数据库连接， Java语言操作数据库

​	JDBC本质： 其实是官方(sun公司)定义的一套操作所有关系型数据库的规则，即接口。各个数据库厂商去实现这套接口，提供数据库驱动jar包。我们可以使用这套接口(JDBC)编程，真正执行的代码时驱动jar包中的实现类。

 2. 快速入门：

    ```java
    // 1. 导入驱动jar包
    
       // 2. 注册驱动
       Class.forName("com.mysql.jdbc.Driver");
       // 3. 获取数据库连接对象
       Connection conn = DriverManager.getConnection("jdbc:mysql://localhost:3306/eesy", "root", "12345678");
    
       // 4. 定义sql语句
       String sql = "update account set money = 500 where id = 1";
    
       // 5. 获取执行sql的对象 Statement
       Statement stmt = conn.createStatement();
    
       // 6. 执行sql
       int count = stmt.executeUpdate(sql);
    
       // 7. 处理结果
       System.out.println(count);
    
       // 8. 释放资源
       stmt.close();
       conn.close();
    ```

    3.详解各个对象

    ​	1. DriverManager: 驱动管理对象

    ​		* 功能：

    ​				1).  注册驱动： 告诉程序该使用哪一个数据库驱动jar

    ​	Driver.java

    ```java
    static {
    
        try {
    
            java.sql.DriverManager.registerDriver(new Driver());
    
        } catch (SQLException E) {
    
            throw new RuntimeException("Can't register driver!");
    
        }
    
    }
    ```

    Class.forName("com.mysql.jdbc.Driver")

    mysql 5 之后可以不注册驱动了  

    #### 因为在mysql-connector-java-5.1.37-bin.jar中META-INF/services/java.sql.Driver 中有com.mysql.jdbc.Driver

    ​                2).   获取数据库连接	 DriverManager.java        236行  

    ```java
    public static Connection getConnection(String url,String user, String password)
    ```

     2.  Connection: 数据库连接对象

        - 功能

          ​	1. 获取执行sql的对象

          ​		 Statement createStatement()

          ​		 PreparedStatement prepareStatement(String sql)

        - 管理事务

          ​	开启事务： void setAutoCommit(boolean autoCommit)  : 调用该方法设置参数为false,即开启事务

          ​	提交事务： commit() :  

          ​	回滚事务： rollback():

        

    3. Statement: 执行sql的对象

        - 执行sql

          1.  boolean execute(String sql) : 可以执行任意的sql

          2.  int executeUpdate(String sql): 执行DML(insert,  update,  delete) 语句,DDL(create, alter, drop)语句

             ​	返回值，影响的行数  > 0 执行成功

          3.  ResultSet executeQuery(String sql): 执行DQL (select)语句

             

          ```java
    Connection conn = null;
          Statement stmt = null;
      
          try {
          // 1. 注册驱动
              Class.forName("com.mysql.jdbc.Driver");
          // 2. 获取连接对象
              conn = DriverManager.getConnection("jdbc:mysql:///eesy", "root", "12345678");
          
              // 3. 定义sql
              String sql = "create table student (id int , name varchar(20))";
              // 4. 获取执行sql对象
          
              stmt = conn.createStatement();
          
              // 5. 执行sql
              int count = stmt.executeUpdate(sql);
          
              // 6. 处理结果
              System.out.println(count);
          
          
          } catch (ClassNotFoundException e) {
              e.printStackTrace();
          }catch (SQLException e) {
              e.printStackTrace();
          }finally {
              // 7 .释放资源
              if(stmt != null) {
                  try {
                      stmt.close();
                  } catch (SQLException e) {
                      e.printStackTrace();
                  }
              }
          
              if(conn != null) {
                  try {
                      conn.close();
                  } catch (SQLException e) {
                      e.printStackTrace();
                  }
              }
          }
          ```
          
             
          
             
    
    4. ResultSet:  结果集对象，封装查询的对象
    
        ​		1. next(): 游标向下移动一行
    
        ​		2. getXxx(): 获取数据
    
        ​					 - Xxx: 代表数据类型  如: int  getInt()  , String getString()
    
        ​					 - 参数
    
        ​								1.int: 代表编号。从1开始     如： getString(1)
    
        ​								2.String : 代表列名称  如： getDouble()			
    
        
    
        
    
        ```java
        	    Connection conn = null;
                Statement stmt = null;
                ResultSet rs = null;
        
                try {
                    // 1. 注册驱动
                    Class.forName("com.mysql.jdbc.Driver");
                    // 2. 获取连接对象
                    conn = DriverManager.getConnection("jdbc:mysql:///eesy", "root", "12345678");
        
                    // 3. 定义sql
                    String sql = "select * from account";
                    // 4. 获取执行sql对象
        
                    stmt = conn.createStatement();
        
                    // 5. 执行sql
                    rs = stmt.executeQuery(sql);
                    
                    // 6. 处理结果
                    //System.out.println(count);
                    // 6.1 让游标向下移动一行
                    rs.next();
                    // 6.2  获取数据
                    int id = rs.getInt(1);
                    String name = rs.getString("name");
                    double money = rs.getDouble(3);
        
                    System.out.println(id + "----" + name + "----" + money);
        
                } catch (ClassNotFoundException e) {
                    e.printStackTrace();
                }catch (SQLException e) {
                    e.printStackTrace();
                }finally {
                    // 7 .释放资源
                    if(rs != null) {
                        try {
                            rs.close();
                        } catch (SQLException e) {
                            e.printStackTrace();
                        }
                    }
                    if(stmt != null) {
                        try {
                            stmt.close();
                        } catch (SQLException e) {
                            e.printStackTrace();
                        }
                    }
        
                    if(conn != null) {
                        try {
                            conn.close();
                        } catch (SQLException e) {
                            e.printStackTrace();
                        }
                    }
        ```
    
        ​					
    
    5. PreparedStatement：执行sql的对象