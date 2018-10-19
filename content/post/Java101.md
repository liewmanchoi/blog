---
title: "Java101"
date: 2018-10-19T17:15:59+08:00
draft: true
lastmod: 2018-10-19T17:15:59+08:00
tags: ["算法工程师", "Java"]
categories: ["Java"]
author: "王圣"
---

### 1.Java程序结构
* Java程序必须以class的形式存在，所有的程序部分都必须位于类定义体中
* 可以被解释器执行的class必须包含main方法，main方法原型：`public static void main(String[] args)`
* 一个源文件内最多包含一个`public`类，而且文件名必须与该public类名相同

### 2.数据类型
* 基本类型primitive type
	* 整型：`int`（4字节）|`short`（2字节）|`long`（8字节，后缀`L`）|`byte`（1字节）
	* 浮点型：`float`（4字节，后缀`F`）|`**double**`（8字节，默认不使用后缀，**常用**）
	* 字符类型：`char`（1字节）
		* `'A'`表示字符常量
		* `"A"`表示字符串
		* **不要在程序中使用char类型**
	* 布尔类型：`false`, `true`
	
### 3.变量
* Java不区分变量的声明和定义
* 关键字`final #f44336`指示常量，如`final double CM+PER_INCH = 2.54`
* 枚举类型：包括有限个命名的值，如`enum Size {SMALL, MEDIUM, LARGE, EXTRA_LARGE};`

### 4.字符串`String`：`不可变对象`
* 每个使用双括号括起来的字符串都是String类的对象
* 当一个字符串使用`+`号与非字符串的值进行拼接时，后者被转换成为字符串。任何一个Java对象都可以通过`toString()`方法转换成字符串
* 字符串字面值是**不可变**的，因此不能进行修改（底层数据结构添加了`final`修饰符）
* 检测两个字符串是否相等必须使用String的`equals()` 方法
	* 不能使用```运算符，这个运算符只能检验两个字符串是否在同一个内存位置上
```java
String greeting = "Hello";
if ("Hello".equals(greeting)) {}
```
* 重要API：
	* `char charAt(int index)` 返回给定位置的字符。类似于C/C++中的[]运算符
	* `int compareTo(String other)` 比较字符串的字典序
	* `boolean equals(Object other)` 判断字符串是否相同
	* `int indexOf(String str)` 返回与str匹配的第一个子串的开始位置
	* `String subString(int begintIndex, int endIndex)` 返回`[beginIndex, endIndex)`的新子字符串
	* `int length()` 返回字符串的长度
	
### 5.使用`StringBuilder`类构建字符串
* String类的拼接+操作会生成许多临时对象，严重影响效率
* 使用`StringBuilder`对象的`append()`方法来扩展字符串
* API：
	* `int length()` 返回StringBuilder对象中的字符串长度
	* `StringBuilder append(String str)` 向StringBuiler对象中追加一个字符串并且返回`this`
	* `void setCharAt(int i, char c)` 将第i个字符设置为c
	* `StringBuilder insert(int offset, String str)` 在offset位置插入str并且返回`this`
	* `StringBuilder delete(int startIndex, endIndex)` 删除范围`[startIndex, endIndex)`中的字符
	* `String toString()` 返回不可变的String对象
	
### 6.输入输出
* 输入：
	* 首先需要构造`Scanner`对象，并与标准输入流`System.in`相关联，即`Scanner in = new Scanner(System.in)`
	* 其次调用下列方法读取内容：
		* `String nextLine()` 读取下一行的内容
		* `String next()` 读取下一个字符串（空格作为分隔符）
		* `int nextInt()` 
		* `double nextDouble()` 读取并转换下一个表示整数或浮点数的字符序列
		* `boolean hasNext()` 检测输入是否还有其他字符串
		* `boolean hasNextInt()/hasNextDouble()` 检测是否还有表示整数或浮点数的下一个字符序列
* 输出：
	* `System.out.printf()` 方法支持类似于C的格式化输出
		* `String.format()` 方法可创建格式化的字符串
		
### 7.操作数组的工具类`Arrays`
* `int binarySearch(type[] a, type key)`  使用二分查找法查询key在数组a中出现的索引；如果a中不包含key，则返回负数；要求数组a已经按照升序排序
* `type[] copyOf(type[] original, int length)`  把数组original复制成一个新数组，其中length是新数组的长度                
* `type copyOfRange(type[] original, int from, int to)`                                       
* `boolean equals(type[] a, type[] b)`  如果数组a和数组b的长度相等，且元素也完全相同，则返回true
* `void fill(type[] a, type val)`  将数组a的所有元素都赋值为val                         
* `void sort(type[] a)`  对数组a的元素进行排序             
* `String toString(type[] a)`   将一个数组转换为字符串，数组元素之间使用英文逗号(,)和空格隔开 