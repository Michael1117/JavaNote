## OOP01

OOPTest.java

```java
package com.shoo.java;

/**
 * 关键字： this、super、static、final、abstract、interface、package、import等
 * 
 * 1.面向过程： 强调的是功能行为，以函数为最小单位，考虑怎么做
 * 
 * 2. 面向对象： 强调具备了功能的对象，以类/对象为最小单位，考虑谁来做。
 * 
 * 3. 面向对象的两个要素：
 * 类： 对一类事物的描述，是抽象、概念上的定义
 * 对象： 是实际存在的该类事物的每一个个体，因而也称为实例(instance)
 * > 面向对象程序设计的重点是类的设计
 * > 设计类，就是设计类的成员
 */

public class OOPTest {
    public static void main(String[] args) {

    }
}
```

PersonTest.java

```java
package com.shoo.java;

/**
 * 一、设计类，其实就是设计类的成员
 * <p>
 * 属性 = 成员变量 = field = 域、字段
 * 方法 = 成员方法 = 函数 = method
 * <p>
 * 创建类的对象 = 类的实例化 = 实例化类
 * <p>
 * 二、类和对象的使用(面向对象思想落地的实现)
 * <p>
 * 1. 创建类，设计类的成员
 * 2. 创建类的对象
 * 3. 通过"对象.属性"或"对象.方法"调用对象的结构
 * <p>
 * 三、如果创建了一个类的多个对象，则每个对象都独立的拥有一套类的属性。(非static的)
 * 意味着： 如果我们修改一个对象的属性a，并不会影响另一个对象属性a的值
 */
public class PersonTest {
    public static void main(String[] args) {

        // 2.创建Person类的对象
        Person p1 = new Person();

        // 调用对象的结构： 属性、方法
        // 调用属性： "对象.属性"
        p1.name = "Tom";
        p1.isMale = true;

        System.out.println(p1.name);

        // 调用方法： "对象.方法"
        p1.eat();
        p1.sleep();

        p1.talk("中文");

        Person p2 = new Person();
        System.out.println(p2.name);
        System.out.println(p2.isMale);

        // 将p1变量保存的对象地址值赋给p3，导致p1和p3都指向了堆空间中的同一个对象实体。
        Person p3 = p1;

        System.out.println(p3.name);  // Tom

        p3.age = 10;

        System.out.println(p1.age);  // 10


    }
}

// 1. 创建类，设计类的成员

class Person {

    // 属性
    String name;
    int age = 1;
    boolean isMale;

    // 方法

    public void eat() {
        System.out.println("人吃饭");
    }

    public void sleep() {
        System.out.println("人要睡觉");
    }

    public void talk(String language) {
        System.out.println("人说话，使用的是：" + language);
    }
}
```

```java
package com.shoo.java;

/**
 * 类中属性的使用
 * <p>
 * 属性 (成员变量)  vs  局部变量
 * <p>
 * 1. 相同点
 * 1.1 定义变量的格式： 数据类型  变量名 = 变量值
 * 1.2 先声明，后使用
 * 1.3 变量都有其对应的作用域
 * <p>
 * 2. 不同点
 * 2.1 在类中声明的位置不同
 * 属性： 直接定义在类的一对{}内
 * 局部变量： 声明在方法内、方法形参、代码块内、构造器形参、构造器内部的变量
 * <p>
 * 2.2 关于权限修饰符的不同
 * 属性： 可以在声明属性时，指明其权限，使用权限修饰符。
 * 常用的权限修饰符： private、public、缺省、protected ---> 封装性
 * 局部变量： 不可以使用权限修饰符
 * <p>
 * 2.3 默认初始化值的情况：
 * 属性： 类的属性，根据其类型，都有默认初始化值。
 * 整型(byte、short、int、long)：0
 * 浮点型(float、double)： 0.0
 * 字符型(char): 0  (或'\u0000')
 * 布尔型(boolean): false
 * <p>
 * 引用数据类型(类、接口、数组):null
 * <p>
 * 局部变量： 没有默认初始化值。
 * 在调用局部变量之前，一定要显式赋值
 * 特别地： 形参在调用时，我们赋值即可
 * 2.4 在内存中加载的位置：
 * 属性： 加载到堆空间中  (非static)
 * 局部变量： 加载到栈空间中
 */
public class UserTest {
    public static void main(String[] args) {
        User u1 = new User();

        System.out.println(u1.name);
        System.out.println(u1.age);
        System.out.println(u1.isMale);

        u1.talk("韩语");
        u1.eat();
    }
}


class User {
    // 属性 (或成员变量)

    String name;
    public int age;
    boolean isMale;

    public void talk(String language) {  // language : 形参，也是局部变量
        System.out.println("我们使用" + language + "进行交流");
    }

    public void eat() {

        String food = "烙饼";

        System.out.println("北方人喜欢吃" + food);
    }
}
```

JavaBean：可重用的组件

```java
package com.shoo.java1;

/**
 * JavaBean是一种Java语言写成的可重用组件
 *      所谓JavaBean，是指符合如下标注的Java类
 *      类是公共的
 *      有一个无参的公共的构造器
 *      有属性，且有对应的get、set方法
 */
public class Customer {
    private int id;
    private String name;
    
    public Customer() {
        
    }
    
    public void setId(int i) {
        id = i;
    }
    
    public int getId() {
        return id; 
    }
    
    public void setName(String n) {
        name = n;
    }
    public String getName() {
        return name;
    }
}
```

PersonTest.java

```java
package com.shoo.java1;

/**
 * 类的结构三： 构造器(或构造方法、constructor)的使用
 * construct: 建设、建造。
 *
 * 一、构造器的作用：
 * 1.创建对象
 * 2.初始化对象的信息
 *
 * 二、说明
 * 1.如果没有显示的定义类的构造器的话，则系统默认提供一个空参的构造器
 * 2.定义构造器的格式 ： 权限修饰符 类名(形参列表) {}
 * 3.一个类中定义的多个构造器，彼此构成重载
 * 4.一旦我们显示的定义了类的构造器之后，系统就不再提供默认的空参构造器
 * 5.一个类中，至少会有一个构造器
 */
public class PersonTest {
    public static void main(String[] args) {
        Person p = new Person();
        //Person p = new Person("Tom");
        p.eat();
        System.out.println(p.name);
        System.out.println(p.age);

        /*Person p1 = new Person("Tom");
        System.out.println(p1.name);

        Person p2 = new Person("Tom", 13);
        System.out.println(p1.age);*/
    }
}


class Person {

    // 属性
    String name;
    int age;

    // 构造器
    public Person() {
        System.out.println("Person().....");
    }

    public Person(String n) {
        name = n;
    }

    public Person(String n, int a) {
        name = n;
        age = a;
    }

    // 方法

    public void eat() {
        System.out.println("人吃饭");
    }

    public void study() {
        System.out.println("人学习");
    }
}
```

UserTest.java

```java
package com.shoo.java1;


/**
 * 总结： 属性赋值的先后顺序
 * ①  默认初始化
 * ②  显示初始化
 * ③  构造器中初始化
 * ④  通过"对象.方法"或"对象.属性"的方式赋值
 *
 * 以上操作的先后顺序 ： ①-②-③-④
 */
public class UserTest {
    public static void main(String[] args) {
        User u = new User();

        System.out.println(u.age);

        User u1 = new User(4);
        System.out.println(u1.age);

        u1.setAge(55);

        System.out.println(u1.age);

    }
}

class User{

    String name;
    int age = 1;

    public User() {

    }

    public User(int a) {
        age = a;
    }

    public void setAge(int a) {
        age = a;
    }
}
```