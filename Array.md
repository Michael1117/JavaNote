## Array

**数组本身是引用数据类型，而数组中的元素可以是任何类型，包括基本数据类型和引用数据类型。**

创建数组对象会在内存中**开辟一整块连续的空间**，而数组名中引用的是这块连续空间的首地址。

数组的**长度一旦确定，就不能修改**。

可以直接通过下标(或索引)的方式调用指定位置的元素，速度很快。

数组的分类

​	按照维度： 一维数组，二维数组，三维数组、.....

​	按照元素的数据类型分： 基本数据类型元素的数组、引用数据类型元素的数组(即对象数组)

### 一维数组的使用： 声明

一维数组的**声明方式：**

​	type var[]或type[] var;

​	例如：

​		int a[]

​		int[] a1;

​		double b[]

​		String[] c; // 引用类型变量数组



Java语言中声明数组时不能指定其长度(数组中元素的数),例如： int a[5]; // 错误

### 一维数组的使用： 初始化

**动态初始化**： 数组声明且为数组元素分配空间与赋值的操作分开进行

int[] arr = new int[3];                       String names[]

arr[0] = 3;								   names = new String[2];

arr[1] = 9;								   names[0] = "张三"

arr[2] = 8;								   names[1] = "李四"

**静态初始化**： 在定义数组的同时就为数组元素分配空间并赋值。

int arr[] = new int[]{3,9,8};                 String names[] = new String{"张三","李四","王五"}

或

int[] arr = {3,9,8};





ArrayTest.java

```java
package com.hefeng.www;


/**
 * 一、数组的概述
 *  1.数组的理解： 数组(Array), 是多个相同类型数据按一定顺序排列的集合，并使用一个名字命名，
 *  并通过编号的方式对这些数据进行统一管理。
 *  2. 数组相关的概念：
 *     > 数组名
 *     > 元素
 *     > 角标、下标、索引
 *     > 数组的长度： 元素的个数
 *
 */
public class ArrayTest {
    public static void main(String[] args) {
        // 1. 一维数组的声明和初始化
        int num; // 声明
        num = 10; // 初始化
        int id = 1001; // 声明 + 初始化

        int[] ids;  // 声明
        // 1.1 静态初始化化： 数组的静态初始化和数组元素的赋值操作同时进行
        ids = new int[]{1001,1002,1003,1004};
        // 1.2 动态初始化： 数组的初始化和数组元素的赋值操作分开进行
        String[] names = new String[5];

        // 也是正确的写法
        int[] arr4 = {1,2,3,4,5};  // 类型推断

        // 总结： 数组一旦初始化完成，其长度就确定了
        names[0] = "张三";
        names[1] = "李四";
        names[2] = "王五";
        names[3] = "Rose";
        names[4] = "Jack";

        // 3 . 获取数组的长度
        System.out.println(names.length);

        int[] ids2 = new int[5];
        System.out.println(ids2.length);
        String[] pass = new String[]{"1","2","2","3","3","3"};
        System.out.println(pass.length);

        for (int i = 0; i < names.length; i++) {
            System.out.println(names[i]);
        }
    }
}
```



ArrayTest1.java

