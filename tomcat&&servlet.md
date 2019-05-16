## tomcat && servlet

![1557638209987](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557638209987.png)

![1557638344464](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557638344464.png)

catalina.bat环境变量

![1557638703075](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557638703075.png)

netstat -ano

conf/server.xml

![1557639545606](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557639545606.png)

![1557639929635](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557639929635.png)

## 2.1 tomcat部署方式一：直接部署到webapps下

![1557640394913](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557640394913.png)

## 直接部署到webapps下war方式，war包自动解压



![1557640205964](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557640205964.png)

## tomcat部署方式二

docBase="D:\hello" 	项目存放路径

path="/hello"	     虚拟目录



![1557640619346](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557640619346.png)



![1557640589164](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557640589164.png)



访问路径 : <http://localhost:8080/hello/hello.html>

![1557640742813](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557640742813.png)

![1557640802111](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557640802111.png)

## 配置方式三：在D:\tomcat\conf\Catalina\localhost创建一个xml文件

访问路径： <http://localhost:8080/bbb/hello.html>

![1557641187719](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557641187719.png)



![1557641162540](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557641162540.png)

### 2.2 tomcat与IDEA集成&创建web项目

![1557641538128](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557641538128.png)

![1557641600673](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557641600673.png)

![1557641689410](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557641689410.png)

## 2.3热部署



![1557642078021](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557642078021.png)

![1557642114260](C:\Users\michaelhee\AppData\Roaming\Typora\typora-user-images\1557642114260.png)

## 3. JSON

* 解析器
  * 常见的解析器： Jsonlib, Gson(Google), fastjson(阿里巴巴),jackson(Spring)

1. JSON转为Java对象

   

2. Java对象转为JSON

   1. 使用步骤：
      1. 导入jackson的jar包
      2. 创建Jackson核心对象 ObjectMapper
      3. 调用ObjectMapper的相关方法

