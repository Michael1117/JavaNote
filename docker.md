## Docker

### 1.1在docker环境下如何为前后端分离项目设计一套**高性能，高负载，高可用**的部署方案？

![1558032285825](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1558032285825.png)

![1558032305642](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1558032305642.png)

![1558032322184](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1558032322184.png)

![1558032337667](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1558032337667.png)

![1558032362076](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1558032362076.png)

单节点的部署方案，某一个节点出现故障，就会造成整个系统宕机。

集群化的部署方案

5节点的mysql集群

6节点的redis集群

3节点的tomcat集群

集群分发请求做负载均衡。

### Haproxy对数据库集群做负载均衡

### nginx对后端和前端做负载均衡

### 为了保证负载均衡的高可用，还会使用keepalived实现双机热备

![1558032791193](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1558032791193.png)

### 改造称为分布式的，云平台的。

### 懂运维，就能很好的理解项目架构的设计，

### 在集群条件下，会存在Tomcat丢失session数据的情况，因为同一个浏览器的两次请求被负载均衡到了不同的tomcat上，所以session不相同了，可以采用redis集中缓存session，防止数据的丢失。



MySQL的PXC集群方案

### 1.2 Docker环境下的前后端分离项目部署与运维项目演示

![1558033180201](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1558033180201.png)

![1558033237616](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1558033237616.png)

高性能，高负载，高可用

比如：以前所有的数据操作都由一个MySQL数据库去处理，压力很大，响应速度很慢，现在使用了数据库集群，由多个数据库节点去处理这些请求，速度快了很多；某一个数据库节点出了问题，出现了宕机，还有其他的节点可以使用。其他的集群也是如此。

### 关闭节点 (docker pause)

关闭数据库节点 node1 node2，由于有5个数据库节点，所以程序依然可以正常运行。

![1558033637974](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1558033637974.png)

关闭redis节点 r1 r2，由于有6个redis节点，所以程序依然可以正常运行。

![1558033700490](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1558033700490.png)



关闭nginx节点

![1558033749678](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1558033749678.png)

关闭tomcat节点

![1558033802209](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1558033802209.png)

### 1.3

![1558033858276](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1558033858276.png)

![1558033878510](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1558033878510.png)

![1558033990497](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1558033990497.png)

在Linux操作系统里，直接安装一些程序，部署一些项目，它们之间可能会有冲突，因此可以安装Docker虚拟机，利用docker虚拟机去创建出很多的空间，在里面部署一些程序，程序与程序之间是完全隔离的。

![1558034261425](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1558034261425.png)

每一个MySQL的节点都要发布到Docker虚拟机的实例里，专有名词容器，每一个MySQL都要部署到独立的容器中，MySQL之间有一个集群的环境。

![1558034594830](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1558034594830.png)

### 1.4

![1558034683067](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1558034683067.png)



![1558034698833](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1558034698833.png)

![1558034724223](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1558034724223.png)

![1558034762896](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1558034762896.png)

![1558034796492](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1558034796492.png)

![1558035146098](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1558035146098.png)

![1558035374554](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1558035374554.png)

### 2.1 

![1558035503292](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1558035503292.png)

![1558035527605](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1558035527605.png)

### 2.2

![1558035671222](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1558035671222.png)

![1558035719105](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1558035719105.png)

权限管理用到的是Shiro技术

后台API调试Swagger

保存，认证和授权信息用JWT

![1558036040814](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1558036040814.png)

只要在任何一个微服务架构的节点上成功登陆，在其他节点上就不需要重新登陆了，这就叫单点登陆功能。

session不能再多个项目中共享，JWT技术不再session里保存认证与授权信息，将信息保存在浏览器上，客户端访问A后端项目，将认证信息发过来，客户端访问B后端项目，也将认证信息发过来。如果发过来的令牌信息无误，则认为登陆成功。

## DataGrip使用

![1558039665968](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1558039665968.png)

![1558039728414](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1558039728414.png)

![1558039767293](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1558039767293.png)

![1558039891739](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1558039891739.png)

application-dev.yml

```yml
spring:
    datasource:
        type: com.alibaba.druid.pool.DruidDataSource
        druid:
            driver-class-name: com.mysql.jdbc.Driver
            url: jdbc:mysql://localhost:3306/renren_fast?allowMultiQueries=true&useUnicode=true&characterEncoding=UTF-8&useSSL=false
            username: root
            password: 12345678
            initial-size: 10
            max-active: 100
            min-idle: 10
            max-wait: 60000
            pool-prepared-statements: true
            max-pool-prepared-statement-per-connection-size: 20
            time-between-eviction-runs-millis: 60000
            min-evictable-idle-time-millis: 300000
            #Oracle需要打开注释
            #validation-query: SELECT 1 FROM DUAL
            test-while-idle: true
            test-on-borrow: false
            test-on-return: false
            stat-view-servlet:
                enabled: true
                url-pattern: /druid/*
                #login-username: admin
                #login-password: admin
            filter:
                stat:
                    log-slow-sql: true
                    slow-sql-millis: 1000
                    merge-sql: false
                wall:
                    config:
                        multi-statement-allow: true


##多数据源的配置
#dynamic:
#  datasource:
#    slave1:
#      driver-class-name: com.microsoft.sqlserver.jdbc.SQLServerDriver
#      url: jdbc:sqlserver://localhost:1433;DatabaseName=renren_security
#      username: sa
#      password: 123456
#    slave2:
#      driver-class-name: org.postgresql.Driver
#      url: jdbc:postgresql://localhost:5432/renren_security
#      username: renren
#      password: 123456
```

项目目录结构

![1558041269881](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1558041269881.png)

![1558041346366](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1558041346366.png)