### 第3章

```java

public class ClassName{
    public static void main(Stirng[] args){
        program statements;
    }
}


```

调用方法

```java
object.method(parameters)
```

byte  short int long

float double



**经常希望某个常量可以在一个类的多个方法中使用，通常将这些常量称为类常量。类常量定义位于main方法的外部。**

```java
package com.shoo;

public class Constants {
    public static final double CM_PER_INCH = 2.54;
    public static void main(String[] args) {


        //final double CM_PER_INCH = 2.54;
        double paperWidth = 8.5;
        double paperHeight = 11;

        System.out.println("Paper size in centimeters: " + paperWidth * CM_PER_INCH + " by " + paperHeight * CM_PER_INCH);
    }
}

```

整数被0除会产生一个异常，而浮点数被0除将会得到无穷大或NaN结果。



println方法处理System.out对象。

Math类中的sqrt方法处理的不是对象，这样的方法被称为静态方法。

```java
double x = 4;
double y = Math.sqrt(x);
System.out.println(y);
```

<<  和 >> 、>>>



0
01
012
0123
01234
012345
0123456
01234567
012345678
0123456789
012345678910

