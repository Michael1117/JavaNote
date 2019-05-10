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

@SpringBootApplication

1.声明一个配置类

```java
package org.springframework.boot;

import java.lang.annotation.Documented;
import java.lang.annotation.ElementType;
import java.lang.annotation.Retention;
import java.lang.annotation.RetentionPolicy;
import java.lang.annotation.Target;

import org.springframework.context.annotation.Configuration;

/**
 * Indicates that a class provides Spring Boot application
 * {@link Configuration @Configuration}. Can be used as an alternative to the Spring's
 * standard {@code @Configuration} annotation so that configuration can be found
 * automatically (for example in tests).
 * <p>
 * Application should only ever include <em>one</em> {@code @SpringBootConfiguration} and
 * most idiomatic Spring Boot applications will inherit it from
 * {@code @SpringBootApplication}.
 *
 * @author Phillip Webb
 * @since 1.4.0
 */
@Target(ElementType.TYPE)
@Retention(RetentionPolicy.RUNTIME)
@Documented
@Configuration
public @interface SpringBootConfiguration {

}

```

2.开启自动配置  

For example, if you have {@code tomcat-embedded.jar} on your classpath you are likely to want a
{@link TomcatServletWebServerFactory} (unless you have defined your own {@link ServletWebServerFactory} bean).

```java
/**
 * Enable auto-configuration of the Spring Application Context, attempting to guess and
 * configure beans that you are likely to need. Auto-configuration classes are usually
 * applied based on your classpath and what beans you have defined. For example, if you
 * have {@code tomcat-embedded.jar} on your classpath you are likely to want a
 * {@link TomcatServletWebServerFactory} (unless you have defined your own
 * {@link ServletWebServerFactory} bean).
 * <p>
 * When using {@link SpringBootApplication}, the auto-configuration of the context is
 * automatically enabled and adding this annotation has therefore no additional effect.
 * <p>
 * Auto-configuration tries to be as intelligent as possible and will back-away as you
 * define more of your own configuration. You can always manually {@link #exclude()} any
 * configuration that you never want to apply (use {@link #excludeName()} if you don't
 * have access to them). You can also exclude them via the
 * {@code spring.autoconfigure.exclude} property. Auto-configuration is always applied
 * after user-defined beans have been registered.
 * <p>
 * The package of the class that is annotated with {@code @EnableAutoConfiguration},
 * usually via {@code @SpringBootApplication}, has specific significance and is often used
 * as a 'default'. For example, it will be used when scanning for {@code @Entity} classes.
 * It is generally recommended that you place {@code @EnableAutoConfiguration} (if you're
 * not using {@code @SpringBootApplication}) in a root package so that all sub-packages
 * and classes can be searched.
 * <p>
 * Auto-configuration classes are regular Spring {@link Configuration} beans. They are
 * located using the {@link SpringFactoriesLoader} mechanism (keyed against this class).
 * Generally auto-configuration beans are {@link Conditional @Conditional} beans (most
 * often using {@link ConditionalOnClass @ConditionalOnClass} and
 * {@link ConditionalOnMissingBean @ConditionalOnMissingBean} annotations).
 */
```

3.扫描包 : 如果没有指定包，扫描将会从声明了注解的包开始,也就是@SpringBootApplication 开始

```java
* <p>Either {@link #basePackageClasses} or {@link #basePackages} (or its alias
* {@link #value}) may be specified to define specific packages to scan. If specific
* packages are not defined, scanning will occur from the package of the
* class that declares this annotation.
```

![1557229426729](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557229426729.png)

BootDemoApplication.java在com目录下，config和web包都在com下，所以都在扫描范围之内。

也可以用@ComponentScan()来配置。



@Configration和@SpringBootApplication的作用基本相同，@SpringBootApplication表示是springboot的注解



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

run->run->SpringApplication

```java
public static final String DEFAULT_REACTIVE_WEB_CONTEXT_CLASS = "org.springframework."
      + "boot.web.reactive.context.AnnotationConfigReactiveWebServerApplicationContext";

private static final String REACTIVE_WEB_ENVIRONMENT_CLASS = "org.springframework."
      + "web.reactive.DispatcherHandler";

private static final String MVC_WEB_ENVIRONMENT_CLASS = "org.springframework."
      + "web.servlet.DispatcherServlet";

private static final String JERSEY_WEB_ENVIRONMENT_CLASS = "org.glassfish.jersey.server.ResourceConfig";
```

```java
public SpringApplication(ResourceLoader resourceLoader, Class<?>... primarySources) {
   this.resourceLoader = resourceLoader;
   Assert.notNull(primarySources, "PrimarySources must not be null");
   this.primarySources = new LinkedHashSet<>(Arrays.asList(primarySources));
   this.webApplicationType = deduceWebApplicationType();
   setInitializers((Collection) getSpringFactoriesInstances(
         ApplicationContextInitializer.class));
   setListeners((Collection) getSpringFactoriesInstances(ApplicationListener.class));
   this.mainApplicationClass = deduceMainApplicationClass();
}

private WebApplicationType deduceWebApplicationType() {
   if (ClassUtils.isPresent(REACTIVE_WEB_ENVIRONMENT_CLASS, null)
         && !ClassUtils.isPresent(MVC_WEB_ENVIRONMENT_CLASS, null)
         && !ClassUtils.isPresent(JERSEY_WEB_ENVIRONMENT_CLASS, null)) {
      return WebApplicationType.REACTIVE;
   }
   for (String className : WEB_ENVIRONMENT_CLASSES) {
      if (!ClassUtils.isPresent(className, null)) {
         return WebApplicationType.NONE;
      }
   }
   return WebApplicationType.SERVLET;
}
```

org.springframework.boot:spring-boot-autoconfigure:2.0.4.RELEASE/org...autoconfigure



aop

cache

dao

data

web

web/servlet/WebMvcAutoConfiguration



AbstractRibbonCommand.class搜索ReadTimeout