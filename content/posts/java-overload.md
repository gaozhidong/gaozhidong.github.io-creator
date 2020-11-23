---
title: "重载（Overload）和重写（Override）的区别"
subtitle: ""
date: 2018-08-19
draft: false
author: "gaozhidong"

description: "重载（Overload）和重写（Override）的区别"

tags: ["Java"]
categories: ["Java"]

featuredImage: ""
featuredImagePreview: ""
---

<!--more-->
## 重载(Overload)

------

**前提**： 所有的重载函数必须在同一个类中

**重载方法的规则：**

1. 参数列表：被重载的方法必须改变参数列表。
2. 返回类型：可以改变返回类型。
3. 修饰符：可以改变修饰符。
4. 异常：可以声明新的或者更广泛的异常。

**其中：**

1. 方法重载是让类以统一的方式处理不同类型数据的一种手段。多个同名函数同时存在，具有不同的参数个数/类型。重载Overloading是一个类中多态性的一种表现。
2. Java的方法重载，就是在类中可以创建多个方法，它们具有相同的名字，但具有不同的参数和不同的定义。调用方法时通过传递给它们的不同参数个数和参数类型来决定具体使用哪个方法, 这就是多态性。
3. 重载的时候，方法名要一样，但是参数类型和个数不一样，返回值类型可以相同也可以不相同。**无法以返回型别作为重载函数的区分标准。**

**同名不同参数**

```
public class Demo{
    public void go(){
         System.out.println("go1");
    }
    public void go(String a){
         System.out.println("go1");
    }
    public void go(String a, String b){
         System.out.println("go1");
    }
}
```



------

## 重写（Override）

**前提**： 继承

**重写的规则：**

1. 参数列表：必须与被重写方法的参数列表完全匹配。
2. 返回类型：必须与超类中被重写的方法中声明的返回类型或子类型完全相同
3. 访问级别：一定不能比被重写方法强，可以比被重写方法的弱。
4. 非检查异常：重写方法可以抛出任何非检查的异常，无论被重写方法是否声明了该异常。
5. 检查异常：重写方法一定不能抛出新的检查异常，或比被重写方法声明的检查异常更广的检查异常。
6. 不能重写标志为final, static的方法。

**其中：**

1. 父类与子类之间的多态性，对父类的函数进行重新定义。如果在子类中定义某方法与其父类有相同的名称和参数，我们说该方法被重写 (Overriding)。在Java中，子类可继承父类中的方法，而不需要重新编写相同的方法。但有时子类并不想原封不动地继承父类的方法，而是想作一定的修改，这就需要采用方法的重写。方法重写又称方法覆盖。
2. 若子类中的方法与父类中的某一方法具有相同的方法名、返回类型和参数表，则新方法将覆盖原有的方法。如需父类中原有的方法，可使用super关键字，该关键字引用了当前类的父类。
3. 子类重写的函数的访问修饰权限不能低于父类的。

**同名同参数**

```
//父类
public class ParentDemo{
    public void go(){
         System.out.println("go1");
    }
    public void go(String a){
         System.out.println("go1");
    }
    public void go(String a, String b){
         System.out.println("go1");
    }	
}

//子类
public class childrenDemo extends ParentDemo{
    public void go(){
         System.out.println("go1");
    }
    public void go(String a){
         System.out.println("go1");
    }
    public void go(String a, String b){
         System.out.println("go1");
    }
}
```

###### 构造器constructor是否可以被重写？

- 父类的私有方法不能被继承，构造器是不能被继承的，所以就不能被重写。在同一个类中，构造器是可以被重载的

------

## 总结

重载和重写（覆盖）。

- 方法的重写（Overriding）和重载（Overloading）是Java多态性的不同表现。
- 重写Overriding是父类与子类之间多态性的一种表现，重载Overloading是一个类中多态性的一种表现。
- 如果在子类中定义某方法与其父类有相同的名称和参数，我们说该方法被重写 (Overriding)。
- 子类的对象使用这个方法时，将调用子类中的定义，对它而言，父类中的定义如同被“屏蔽”了，而且如果子类的方法名和参数类型和个数都和父类相同，那么子类的返回值类型必须和父类的相同；
- 如果在一个类中定义了多个同名的方法，它们或有不同的参数个数或有不同的参数类型，则称为方法的重载(Overloading)。
- Overloaded的方法是可以改变返回值的类型。也就是说，重载的返回值类型可以相同也可以不同。

