## springboot初始目录结构

![1557219925968](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557219925968.png)

pom.xml

```java
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.hefeng.demo</groupId>
    <artifactId>springboot-demo</artifactId>
    <version>1.0.0-SNAPSHOT</version>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.0.4.RELEASE</version>
    </parent>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid</artifactId>
            <version>1.1.6</version>
        </dependency>
    </dependencies>
</project>
```

jdbp.properties

```java
jdbc.driverClassName=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql:///yun6
jdbc.username=root
jdbc.password=12345678
```

jdbcConfig.java

```java
package com.hefeng.config;

import com.alibaba.druid.pool.DruidDataSource;
import org.springframework.beans.factory.annotation.Value;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;
import org.springframework.context.annotation.PropertySource;

import javax.sql.DataSource;

@Configuration
@PropertySource("classpath:jdbc.properties")
public class JdbcConfig {

    @Value("${jdbc.url}")
    String url;
    @Value("${jdbc.driverClassName}")
    String driverClassName;
    @Value("${jdbc.username}")
    String username;
    @Value("${jdbc.password}")
    String password;

    @Bean
    public DataSource dataSource() {
        DruidDataSource datasource = new DruidDataSource();
        datasource.setDriverClassName(driverClassName);
        datasource.setUrl(url);
        datasource.setUsername(username);
        datasource.setPassword(password);
        return datasource;
    }
}
```

BootDemoApplication.java

```java
package com.hefeng;

import org.springframework.boot.SpringApplication;
import org.springframework.boot.autoconfigure.SpringBootApplication;

@SpringBootApplication
public class BootDemoApplication {
    public static void main(String[] args) {
        SpringApplication.run(BootDemoApplication.class, args);
    }
}
```

HelloController.java

```java
package com.hefeng.web;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.stereotype.Controller;
import org.springframework.web.bind.annotation.GetMapping;
import org.springframework.web.bind.annotation.ResponseBody;

import javax.sql.DataSource;

@Controller
public class HelloController {
    @Autowired
    private DataSource dataSource;

    @GetMapping("hello")
    @ResponseBody
    public String hello() {
        return "hello, spring boot!";
    }
}
```

maven配置

![1557220181236](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557220181236.png)

![1557220264309](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557220264309.png)

项目启动

![1557220330125](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557220330125.png)



### springBoot配置方式一

目录结构

![1557224463413](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557224463413.png)

将jdbc.properties改为application.properties

application.properties

```java
jdbc.driverClassName=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql:///yun6
jdbc.username=root
jdbc.password=12345678
```

JdbcProperties.java

```java
package com.hefeng.config;
import lombok.Data;
import org.springframework.boot.context.properties.ConfigurationProperties;

@ConfigurationProperties(prefix = "jdbc")
@Data
public class JdbcProperties {
    String url;
    String driverClassName;
    String username;
    String password;
}
```



JdbcConfig.java

```java
package com.hefeng.config;

import com.alibaba.druid.pool.DruidDataSource;
import org.springframework.beans.factory.annotation.Autowired;
import org.springframework.boot.context.properties.EnableConfigurationProperties;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

import javax.sql.DataSource;

@Configuration
@EnableConfigurationProperties(JdbcProperties.class)
public class JdbcConfig {
    @Autowired
    @Bean
    public DataSource dataSource(JdbcProperties prop) {
        DruidDataSource datasource = new DruidDataSource();
        datasource.setDriverClassName(prop.getDriverClassName());
        datasource.setUrl(prop.getUrl());
        datasource.setUsername(prop.getUsername());
        datasource.setPassword(prop.getPassword());
        return datasource;
    }
}
```

pom.xml (需要下载插件lombok)

```java
<?xml version="1.0" encoding="UTF-8"?>
<project xmlns="http://maven.apache.org/POM/4.0.0"
         xmlns:xsi="http://www.w3.org/2001/XMLSchema-instance"
         xsi:schemaLocation="http://maven.apache.org/POM/4.0.0 http://maven.apache.org/xsd/maven-4.0.0.xsd">
    <modelVersion>4.0.0</modelVersion>

    <groupId>com.hefeng.demo</groupId>
    <artifactId>springboot-demo</artifactId>
    <version>1.0.0-SNAPSHOT</version>

    <parent>
        <groupId>org.springframework.boot</groupId>
        <artifactId>spring-boot-starter-parent</artifactId>
        <version>2.0.4.RELEASE</version>
    </parent>

    <dependencies>
        <dependency>
            <groupId>org.springframework.boot</groupId>
            <artifactId>spring-boot-starter-web</artifactId>
        </dependency>
        <dependency>
            <groupId>com.alibaba</groupId>
            <artifactId>druid</artifactId>
            <version>1.1.6</version>
        </dependency>
        <dependency>
            <groupId>org.projectlombok</groupId>
            <artifactId>lombok</artifactId>
        </dependency>
    </dependencies>
</project>
```

### springboot第二种属性注入方式

目录结构

![1557225998914](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557225998914.png)



JdbcConfig.java

```java
package com.hefeng.config;

import com.alibaba.druid.pool.DruidDataSource;
import org.springframework.boot.context.properties.ConfigurationProperties;
import org.springframework.context.annotation.Bean;
import org.springframework.context.annotation.Configuration;

import javax.sql.DataSource;

@Configuration
public class JdbcConfig {
    @Bean
    @ConfigurationProperties(prefix = "jdbc")
    public DataSource dataSource() {
        return new DruidDataSource();
    }
}
```

JdbcProperties.java (注意JdbcProperties.java中的属性要和application.properties中一一对应)

```java
package com.hefeng.config;
import lombok.Data;

@Data
public class JdbcProperties {
    String url;
    String driverClassName;
    String username;
    String password;
}
```

application.properties

```java
jdbc.driverClassName=com.mysql.jdbc.Driver
jdbc.url=jdbc:mysql:///yun6
jdbc.username=root
jdbc.password=12345678
```

![1557225899744](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557225899744.png)

pom.xml没有变化。

第一种属性注入方式适用于很多地方使用，配置相对较复杂

第二种适用于自己使用，配置更简单



application.yml和application.yaml都可以

application.yaml

```yaml
jdbc:
  driverClassName: com.mysql.jdbc.Driver
  url:jdbc: mysql:///yun6
  username: root
  password: 12345678
  user:
    name: jack
    age: 2
    language:
      - java
      - php
      - ios
      - python
      - scala
      
```

JdbcProperties.java   yaml 属性注解

```java
package com.hefeng.config;
import lombok.Data;

import java.util.List;

//@ConfigurationProperties(prefix = "jdbc")
@Data
public class JdbcProperties {
    String url;
    String driverClassName;
    String username;
    String password;
    User user = new User();

    class User{
        String name;
        int age;
        List<String> language;
    }
}
```



application.properties和application.yaml都存在的情况下，取并集。

目录结构

![1557227408139](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557227408139.png)