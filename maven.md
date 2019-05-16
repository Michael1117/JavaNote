## Maven

一键构建：使用maven自身集成的tomcat插件，对项目进行构建。

执行mvn clean，没有target目录了。

![1557281925458](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557281925458.png)



执行mvn compile，出现target目录

![1557282041876](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557282041876.png)

mvn compile将main/src目录下的java文件，编译成target/classes下的可执行文件。



mvn test: target目录下生成一个test-classes。它包含了mvn compile。

![1557282340625](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557282340625.png)

执行mvn package，target目录下多了maven-archiver，maven-helloworld-0.0.1-SNAPSHOT，maven-helloworld-0.0.1-SNAPSHOT.war



![1557282719130](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557282920177.png)

mvn install命令，war包重新编译打包。并在C:\java\maven_repository下生成项目

mvn install 命令，执行了compile后，也执行了test,然后执行了package所做的工作，最后把war包安装到本地仓库C:\java\maven_repository下。

war包在  C:\java\maven_repository\cn\itcast\maven\maven-helloworld\0.0.1-SNAPSHOT下。

![1557283255506](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557283255506.png)



![1557283348949](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557283348949.png)

一键构建：使用maven自身集成的tomcat插件，对项目进行构建。

清除项目编译信息		编译		测试		打包		安装		发布

clean				compile	test		package	install	deploy

deploy需要配置。

![1557285198825](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557285198825.png)

Maven基础-概念模型

![1557285313350](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557285313350.png)





-DarchetypeCatalog=internal 不能联网的情况下，如果之前下载过的maven插件，就不用再去网络上去下载，直接加载本地。

![1557286021142](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557286021142.png)

### 创建Maven工程 -- 使用骨架

![1557286305270](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557286305270.png)

![1557286406302](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557286406302.png)

![1557286470120](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557286511850.png)

![1557286587118](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557286587118.png)





![1557287075694](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557287122465.png)

### 创建Maven工程 -- 不使用骨架

![1557287339191](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557287339191.png)

![1557287398213](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557287427624.png)

![1557287451910](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557287451910.png)

目录结构

![1557287509926](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557287509926.png)

### 使用骨架创建maven的web工程

![1557287608174](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557287623895.png)

![1557287665728](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557287665728.png)

![1557287718017](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557287718017.png)

![1557287763973](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557287763973.png)

### 初始目录结构

![1557287831539](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557287831539.png)

main下创建java文件夹

![1557287974898](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557287974898.png)

java目录下无法创建jsp页面，点击File，选择Project Structure。

![1557288425036](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557288425036.png)

![1557288490552](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557288490552.png)

![1557288547396](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557288547396.png)

搜索jar包，maven中央仓库网址  

<https://mvnrepository.com/>



tomcat:run

![1557289669479](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557289669479.png)

pom.xml下有servelt和jsp，tomcat中也有，发生了冲突。

![1557289929151](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557289929151.png)



```java
<dependency>
  <groupId>javax.servlet.jsp</groupId>
  <artifactId>jsp-api</artifactId>
  <version>2.2</version>
  <scope>provided</scope>
</dependency>
```

![1557290107370](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557290107370.png)

maven默认为tomcat 6, tomcat 7配置

```java
<plugin>
  <groupId>org.apache.tomcat.maven</groupId>
  <artifactId>tomcat7-maven-plugin</artifactId>
  <version>2.2</version>
  <configuration>
    <port>8888</port>
  </configuration>
</plugin>
```



创建Live Templates : 输入tomcat 7即可创建模板

![1557292808512](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557292808512.png)

![1557292878429](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557292878429.png)



jdk 8.0 配置

```xml
<plugin>
  <groupId>org.apache.maven.plugins</groupId>
  <artifactId>maven-compiler-plugin</artifactId>
  <configuration>
    <target>1.8</target>
    <source>1.8</source>
    <encoding>UTF-8</encoding>
  </configuration>
</plugin>
```



scope: provided:  servlet-api,jsp-api

scope: runtime: JDBC驱动

scope: test :  Junit



tomcat7:run

