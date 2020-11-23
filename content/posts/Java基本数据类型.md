---
title: "Java基本数据类型"
subtitle: ""
date: 2018-02-18
draft: true
author: "gaozhidong"

description: "Java基本数据类型"

tags: ["Java"]
categories: ["Java"]

featuredImage: ""
featuredImagePreview: ""
---

<!--more-->
**基本数据类型有：**
* byte      字节型
* short     短整型
* int       整型
* long      长整型
* float     单精度浮点
* double     双精度浮点
* char       字符型
* boolean    布尔型

可以分为三类： 

1. 数值类型：**byte**、 **short**、 **int**、 **long**、 **float**、 **double**
2. 字符类型：**char**
3. 布尔型：**boolean**


**byte**

1、byte是8位的数据类型，占用一个字节（8bit)，默认值是0，它的取值范围是(-2^7) ~ (2^7-1)，也就是 -128 ~ 127之间，所以最大存储数据量是255;

2、byte一般在大型数组中使用，来代替整数，因为byte变量占用的空间只有int的1/4

**short**

1、short是16位的数据类型，占用2个字节，默认值是0，它的取值范围是(-2^15) ~(2^15-1)，也就是 -32768 ~ 32767之间，所以最大数据存储量是65536;

2、short虽然是int型变量所占空间的1/2，但是在实际中却很少用到。在大型数组中也可以节省空间。


**int**

1、int是32位的数据类型，占用4个字节，默认值是0，它的取值范围是(-2^31) ~(2^31-1)，也就是 -2147483648 ~ 2147483647之间，所以最大数据存储量是2^32-1;

2、int是数据类型是整型，是我们在项目中用到最多的数据类型之一;

**long**

1、long是64位的数据类型，占用8个字节，默认值是0L，它的取值范围是(-2^63) ~(2^63-1)，也就是 -9223372036854775808 ~ 9223372036854775808之间，所以最大数据存储量是2^64;

2、long是数据类型是长整型，是我们在项目中用到最多的数据类型之一。在使用long类型的数据时最好在数值末尾带上大写的L！

3、long 使用示例:long a=1000L,long b=-2000L;

**float**

1、float是32位的数据类型，占用4个字节，默认值是0，它的取值范围是3.4e-45 ~ 1.4e38 之间;

2、float是数据类型是单精度，在直接赋值时必须在数字后加上f或F。

3、float使用示例:float a=10.25f, float b=-20.35F;

**double**

1、double是64位的数据类型，占用8个字节，默认值是0，它的取值范围是4.9e-324 ~ 1.8e308 之间;

2、double是数据类型是双精度，在直接赋值的时候最好加上D或d。

3、double使用示例:double a=10.123d, double b= -10.25644D;

**boolean**

1、boolean是布尔类型，占用1个字节，只有两个值,false和true，默认值是 false。

2、boolean只能用一种标志来记录 true或false，一般和 if 结合使用。

3、boolean使用示例: boolean a=true，boolean b=false;

**char**

1、char是字符类型，占用2个字节，默认值为空，取值范围 为 0~65535，也就是 \u0000 ~ \uffff。

2、char数据类型可以储存任何字符。

3、char 使用示例: char a=1，char b='A';