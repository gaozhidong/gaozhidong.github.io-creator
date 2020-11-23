---
title: "Java语句和循环"
subtitle: ""
date: 2018-02-22
draft: true
author: "gaozhidong"

description: "Java语句和循环"

tags: ["Java"]
categories: ["Java"]

featuredImage: ""
featuredImagePreview: ""
---

<!--more-->

### 条件语句

##### if-else语法

- if-else语法，只有一个语句被执行
- if和else都是Java中的关键字

```
if(boolean 值){
    if语句块
}else{
    else语句块
}
if(boolean 值){
    if语句块
}else if(){
    if语句块
}else{
    else语句块
}
```

##### switch case 语句判断一个变量与一系列值中某个值是否相等，每个值称为一个分支。

```
switch(expression){
    case value :
       //语句
       break; //可选
    case value :
       //语句
       break; //可选
    //你可以有任意数量的case语句
    default : //可选
       //语句
}

```

## 循环结构

顺序结构的程序语句只能被执行一次。如果您想要同样的操作执行多次,，就需要使用循环结构。

Java中有三种主要的循环结构：

##### while 循环

```
while( 布尔表达式 ) {
  //循环内容
}

public class Test {
   public static void main(String args[]) {
      int x = 10;
      while( x < 20 ) {
         System.out.print("value of x : " + x );
         x++;
         System.out.print("\n");
      }
   }
}
```

##### do…while 循环

对于 while 语句而言，如果不满足条件，则不能进入循环。但有时候我们需要即使不满足条件，也至少执行一次。

do…while 循环和 while 循环相似，不同的是，do…while 循环至少会执行一次。

```
do {
       //代码语句
}while(布尔表达式);

public class Test {
   public static void main(String args[]){
      int x = 10;
 
      do{
         System.out.print("value of x : " + x );
         x++;
         System.out.print("\n");
      }while( x < 20 );
   }

```

##### for 循环

- 让程序在满足某条件时，重复执行某个代码块。for是Java中的关键字

```
for(初始化; 循环体条件表达式; 循环体后语句) {
    //代码语句
}

public class Example {

    //for 循环
    public static void main(String[] args) {
        for (int i = 1; i <= 9; i++) {
            String line = "";
            for (int j = 1; j <= 9; j++) {
                if (j > i) {
                    break;
                }
                line += i + "*" + j + "=" + (i * j) + "\t";
            }
            System.out.println(line);
        }
    }
}

public class Example {

    //for 循环
    public static void main(String[] args) {
        for (int i = 1; i <= 9; i++) {
            for (int j = 1; j <= i; j++) {
                System.out.printIn(i + "*" + j + "=" + (i * j) + "\t")
            }
        }
        System.out.printIn('\n')
    }
}

```