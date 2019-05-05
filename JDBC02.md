## JDBC02

### 数据库连接池

1.概念： 就是一个容器(集合),存放数据库连接的容器。

**当系统初始化好后，容器被创建，容器中会申请一些连接对象，当用户来访问数据库时，从容器中获取连接对象，用户访问完后，会将对象归还给容器。**

2.好处：

​	1.节约资源

​	2.用户访问高效

3.实现

 1. 标准接口： DataSource  javax.sql包下的

    ​	1.方法

    ​		获取连接： getConnection()

    ​		归还连接： **如果连接对象Connetion是从连接池中获取的，那么调用Connection.close()方法，就不会关闭连接，而是归还连接**

    

    ​     2.数据库厂商实现

    ​		1.C3P0 : 数据库连接技术

    ​			c3p0-config.xml

    ​	

    ```java
    <c3p0-config>
      <!-- 使用默认的配置读取连接池对象 -->
      <default-config>
       <!--  连接参数 -->
        <property name="driverClass">com.mysql.jdbc.Driver</property>
        <property name="jdbcUrl">jdbc:mysql://localhost:3306/db4</property>
        <property name="user">root</property>
        <property name="password">12345678</property>
        
        <!-- 连接池参数 -->
        <!--初始化申请的连接数量-->
        <property name="initialPoolSize">5</property>
        <!--最大的连接数量 最多10个连接池对象 -->
        <property name="maxPoolSize">10</property>
        <!--超时时间-->
        <property name="checkoutTimeout">3000</property>
      </default-config>
    
      <named-config name="otherc3p0"> 
        <!--  连接参数 -->
        <property name="driverClass">com.mysql.jdbc.Driver</property>
        <property name="jdbcUrl">jdbc:mysql://localhost:3306/db3</property>
        <property name="user">root</property>
        <property name="password">12345678</property>
        
        <!-- 连接池参数 -->
        <property name="initialPoolSize">5</property>
        <property name="maxPoolSize">8</property>
        <property name="checkoutTimeout">1000</property>
      </named-config>
    </c3p0-config>
    ```

    ​		2.Druid（德鲁伊）：数据库连接技术 (阿里巴巴实现)

    ​			druid.properties

    ```java
    driverClassName=com.mysql.jdbc.Driver
    url=jdbc:mysql:///db3
    username=root
    password=12345678
    # 初始化连接数量
    initialSize=5
    # 最大连接数
    maxActive=10
    # 最大等待时间
    maxWait=3000
    ```

项目目录结构

![1557044617823](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557044617823.png)

DruidDemo.java

```java
package com.hefeng.datasource.druid;

import com.alibaba.druid.pool.DruidDataSourceFactory;

import javax.sql.DataSource;
import java.io.IOException;
import java.io.InputStream;
import java.sql.Connection;
import java.util.Properties;

/**
 * Druid演示
 */
public class DruidDemo {
    public static void main(String[] args) throws Exception {

        // 1. 导入jar包
        // 2. 定义配置文件  druid.properties
        // 3. 加载配置文件
        Properties pro = new Properties();
        InputStream is = DruidDemo.class.getClassLoader().getResourceAsStream("druid.properties");
        pro.load(is);
        // 4. 获取连接池对象  通过工厂来获取 DruidDataSourceFactory

        DataSource ds = DruidDataSourceFactory.createDataSource(pro);

        // 5. 获取连接
        Connection conn = ds.getConnection();
        System.out.println(conn);
    }
}
```

2. 定义一个工具类

      1.定义一个类

      2.通过静态代码块加载配置文件，初始化连接池对象

      3.通过方法

   ​     	1 .   获取连接方法： 通过数据库连接池获取连接

   ​		 2.   释放资源

   ​		 3.    获取连接池的方法	