## mybatis



mybatis目录结构

![1557475931469](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557475931469.png)

User.java

```java
package com.shoo.domain;

import java.io.Serializable;
import java.util.Date;

/**
 *
 */
public class User implements Serializable {
    private Integer id;
    private String username;
    private Date birthday;
    private String sex;
    private String address;

    public Integer getId() {
        return id;
    }

    public void setId(Integer id) {
        this.id = id;
    }

    public String getUsername() {
        return username;
    }

    public void setUsername(String username) {
        this.username = username;
    }

    public Date getBirthday() {
        return birthday;
    }

    public void setBirthday(Date birthday) {
        this.birthday = birthday;
    }

    public String getSex() {
        return sex;
    }

    public void setSex(String sex) {
        this.sex = sex;
    }

    public String getAddress() {
        return address;
    }

    public void setAddress(String address) {
        this.address = address;
    }

    @Override
    public String toString() {
        return "User{" +
                "id=" + id +
                ", username='" + username + '\'' +
                ", birthday=" + birthday +
                ", sex='" + sex + '\'' +
                ", address='" + address + '\'' +
                '}';
    }
}
```

 IUserDao.java (接口)

```java
package com.shoo.dao;

import com.shoo.domain.User;

import java.util.List;

/**
 * 用户的持久层接口
 */
public interface IUserDao {
    List<User> findAll();
}
```

SqlMapConfig.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<!--mybatis主配置文件-->
<configuration>
    <!--配置环境-->
    <environments default="mysql">
        <!--配置mysql的环境-->
        <environment id="mysql">
            <!--配置事务的类型-->
            <transactionManager type="JDBC"></transactionManager>
            <!--配置数据源(连接池)-->
            <dataSource type="POOLED">
                <!--配置连接数据库的4个基本信息-->
                <property name="driver" value="com.mysql.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql://localhost:3306/eesy"/>
                <property name="username" value="root"/>
                <property name="password" value="12345678"/>
            </dataSource>
        </environment>
    </environments>

    <!--指定映射配置文件的位置，映射配置文件指的是每个dao独立的配置文件-->
    <mappers>
        <mapper resource="com/shoo/dao/IUserDao.xml"></mapper>
    </mappers>
</configuration>
```



IUserDao.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
 <mapper namespace="com.shoo.dao.IUserDao">
    <!--配置查询所有 dao中的方法名称-->
    <select id="findAll">
        select * from user
    </select>
</mapper>
```

![1557477281014](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557477281014.png)

MybatisTest.java

```java
package com.shoo;

import com.shoo.dao.IUserDao;
import com.shoo.domain.User;
import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;
import java.io.IOException;
import java.io.InputStream;
import java.util.List;

/**
 * mybatis的入门案例
 */
public class MybatisTest {
    public static void main(String[] args) throws IOException {
        // 1. 读取配置文件
        InputStream in = Resources.getResourceAsStream("SqlMapConfig.xml");
        // 2. 创建SqlSessionFactory工厂
        SqlSessionFactoryBuilder builder = new SqlSessionFactoryBuilder();
        SqlSessionFactory factory = builder.build(in);
        // 3. 使用工厂生产SqlSession对象
        SqlSession session = factory.openSession();
        // 4. 使用SqlSession创建Dao接口的代理对象
        IUserDao userDao = session.getMapper(IUserDao.class);
        // 5. 使用代理对象执行方法
        List<User> users = userDao.findAll();
        for (User user : users) {
            System.out.println(user);
        }
        // 6. 释放资源
        session.close();
        in.close();
    }
}
```

IUserDao.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE mapper
        PUBLIC "-//mybatis.org//DTD Mapper 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-mapper.dtd">
 <mapper namespace="com.shoo.dao.IUserDao">
    <!--配置查询所有 dao中的方法名称-->
    <select id="findAll" resultType="com.shoo.domain.User">
        select * from user
    </select>
</mapper>
```

## 方式二： 注解

![1557479921708](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557479921708.png)

IUserDao.java

```java
package com.shoo.dao;

import com.shoo.domain.User;
import org.apache.ibatis.annotations.Select;

import java.util.List;

/**
 * 用户的持久层接口
 */
public interface IUserDao {
    /**
     * 查询所有操作
     * @return
     */
    @Select("select * from user")
    List<User> findAll();
}
```

SqlMapConfig.xml

```xml
<?xml version="1.0" encoding="UTF-8"?>
<!DOCTYPE configuration
        PUBLIC "-//mybatis.org//DTD Config 3.0//EN"
        "http://mybatis.org/dtd/mybatis-3-config.dtd">
<!--mybatis主配置文件-->
<configuration>
    <!--配置环境-->
    <environments default="mysql">
        <!--配置mysql的环境-->
        <environment id="mysql">
            <!--配置事务的类型-->
            <transactionManager type="JDBC"></transactionManager>
            <!--配置数据源(连接池)-->
            <dataSource type="POOLED">
                <!--配置连接数据库的4个基本信息-->
                <property name="driver" value="com.mysql.jdbc.Driver"/>
                <property name="url" value="jdbc:mysql://localhost:3306/eesy"/>
                <property name="username" value="root"/>
                <property name="password" value="12345678"/>
            </dataSource>
        </environment>
    </environments>

    <!--指定映射配置文件的位置，映射配置文件指的是每个dao独立的配置文件
        如果使用注解来配置的话，此处应该使用class属性指定被注解的dao全限定类名
    -->
    <mappers>
        <mapper class="com.shoo.dao.IUserDao"></mapper>
    </mappers>
</configuration>
```





## 方式三：代理dao实现

MybatisTest.java

```java
package com.shoo;

import com.shoo.dao.IUserDao;
import com.shoo.dao.impl.UserDaoImpl;
import com.shoo.domain.User;
import org.apache.ibatis.io.Resources;
import org.apache.ibatis.session.SqlSessionFactory;
import org.apache.ibatis.session.SqlSessionFactoryBuilder;
import java.io.IOException;
import java.io.InputStream;
import java.util.List;

/**
 * mybatis的入门案例
 */
public class MybatisTest {
    public static void main(String[] args) throws IOException {
        // 1. 读取配置文件
        InputStream in = Resources.getResourceAsStream("SqlMapConfig.xml");
        // 2. 创建SqlSessionFactory工厂
        SqlSessionFactoryBuilder builder = new SqlSessionFactoryBuilder();
        SqlSessionFactory factory = builder.build(in);
        // 3. 使用工厂创建dao的对象
        IUserDao userDao = new UserDaoImpl(factory);

        // 4. 使用代理对象执行方法
        List<User> users = userDao.findAll();
        for (User user : users) {
            System.out.println(user);
        }
        // 5. 释放资源
        in.close();
    }
}
```

UserDaoImpl.java

```java
package com.shoo.dao.impl;

import com.shoo.dao.IUserDao;
import com.shoo.domain.User;
import org.apache.ibatis.session.SqlSession;
import org.apache.ibatis.session.SqlSessionFactory;

import java.util.List;

public class UserDaoImpl implements IUserDao {
    private SqlSessionFactory factory;

    public UserDaoImpl(SqlSessionFactory factory) {
        this.factory = factory;
    }

    public List<User> findAll() {
        // 1. 使用工厂创建SqlSession对象

        SqlSession session = factory.openSession();
        // 2. 使用session执行查询所有方法
        List<User> users = session.selectList("com.shoo.dao.IUserDao.findAll");
        session.close();
        // 3. 返回查询结果
        return users;
    }
}

```

IUserDao.java

```java
package com.shoo.dao;

import com.shoo.domain.User;
import java.util.List;

/**
 * 用户的持久层接口
 */
public interface IUserDao {
    /**
     * 查询所有操作
     * @return
     */

    List<User> findAll();
}
```

```xml
 <!--根据名称模糊查询用户-->
    <select id="findByName" parameterType="string" resultType="com.shoo.domain.User">
    	select * from user where username like #{name};   // 带有预处理
        select * from user where username like '%${value}%' // 没有预处理
    </select>
```