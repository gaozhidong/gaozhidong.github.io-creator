---
title: "Java运算符"
subtitle: ""
date: 2018-03-09
draft: true
author: "gaozhidong"

description: "Java运算符"

tags: ["Java"]
categories: ["Java"]

featuredImage: ""
featuredImagePreview: ""
---

<!--more-->

- 运算符对一个或者多个值进行运算，并得出一个运算结果
- 运算符的运算结果类型有的是固定的，有时候会根据被计算的值变化。比如两个int想加，结果类型就是int。两个byte相加，返回值就是byte。

#### 算术运算符

算术运算符用在数学表达式中，它们的作用和在数学中的作用一样。有加减乘除，取余，自加自减。

```
public class Test {
 
  public static void main(String[] args) {
     int a = 10;
     int b = 20;
     int c = 25;
     int d = 25;
     System.out.println("a + b = " + (a + b) );
     System.out.println("a - b = " + (a - b) );
     System.out.println("a * b = " + (a * b) );
     System.out.println("b / a = " + (b / a) );
     System.out.println("b % a = " + (b % a) );
     System.out.println("c % a = " + (c % a) );
     System.out.println("a++   = " +  (a++) );
     System.out.println("a--   = " +  (a--) );
     // 查看  d++ 与 ++d 的不同
     System.out.println("d++   = " +  (d++) );
     System.out.println("++d   = " +  (++d) );
  }
}
```

#### 关系运算符

```
    ==  //是否相等 如果相等则条件为真
    !=  //是否相等 如果值不相等则条件为真
    >   //检查左操作数的值是否大于右操作数的值，如果是那么条件为真。
    <   //检查左操作数的值是否小于右操作数的值，如果是那么条件为真。
    <=  //检查左操作数的值是否小于或等于右操作数的值，如果是那么条件为真。
    >=  //检查左操作数的值是否大于或等于右操作数的值，如果是那么条件为真。
```


#### 逻辑运算符

逻辑运算符有 **&&** 逻辑与, **||** 逻辑或， **!** 逻辑非。

```
public class Test {
  public static void main(String[] args) {
     boolean a = true;
     boolean b = false;
     System.out.println("a && b = " + (a&&b));
     System.out.println("a || b = " + (a||b) );
     System.out.println("!(a && b) = " + !(a && b));
  }
}
```


#### 赋值运算符

常用到的赋值运算符有 **=** 等于 **+=** 加等于 **-=** 减等于 ***=** 乘等于 **/=** 除等于 等等。



####  其他运算符

    - 条件运算符（三元运算符）
    - instanceof 运算符


​    
​    

#### 运算符优先级

- ()
- !
- *,/,%
- +,-
- <=,<,>=,>
- ==
- !=
- &,&&,|,||
- =


#### 位运算符

 Java定义了位运算符，应用于整数类型(int)，长整型(long)，短整型(short)，字符型(char)，和字节型(byte)等类型。
 位运算符主要针对二进制，它包括了：“与”、“非”、“或”、“异或”。从表面上看似乎有点像逻辑运算符，但逻辑运算符是针对两个关系运算符来进行逻辑运算，而位运算符主要针对两个二进制数的位进行逻辑运算。
