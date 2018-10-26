---
title: "接口、lambda表达式与内部类"
date: 2018-10-26T10:49:05+08:00
draft: false
lastmod: 2018-10-26T10:49:05+08:00
tags: ["算法工程师", "Java"]
categories: ["Java"]
author: "王圣"
---

### 1. 接口
* 接口的特性：接口不是类，用于描述类应该具有什么样的功能
	* 接口中所有的方法都属于`public`。声明方法时，不需要提供`public`关键字
	* 接口不能含有非静态成员变量，只能含有静态常量。所有变量会被自动设为`public static final`
	* 接口不能实例化，但是能声明接口的变量，接口变量必须引用实现了接口的类的对象
	* 每个类可以实现多个接口，变相地实现多重继承
	* 接口可以含有静态方法
	* 接口可以含有默认方法，使用`default`修饰该方法
		* 默认方法可以调用接口中的其他方法
		* 默认方法冲突的解决：
			* **父类优先**：如果父类提供了一个具体方法，函数签名相同的接口默认方法将会被忽略
			* **接口冲突** ：如果一个父接口提供了一个默认方法，另一个父接口也提供了一个签名相同的默认方法，则程序员必须通过覆盖这个默认方法来解决冲突
			
			 ```java
			public interface Collection {
				int size();
				default boolean isEmpty() {
					return size() == 0;
				}
			}
			```
* 接口与抽象类的差别：
	* 类可以实现多个接口，但是只能继承自1个抽象类
	* 接口不含非静态成员变量
* 标记接口tagging interface：如`Cloneable`，标记接口不含有任何方法，唯一的作用就是允许在类型查询中使用`instanceof`

### 2. lambda表达式
* lambda表达式的基础语法：参数、箭头->以及表达式

``` java
(String first, String second) -> {
	if (first.length() < second.length())
		return -1;
	else if (first.length() > second.length())
		return 1;
	else
		return 0;
}
```

* 说明：
	* 如果可以推导出lambda表达式的参数类型，则可以忽略其类型
	* 即便lamda表达式没有参数，仍然要提供空括号
	`() -> { for (int i = 100; i >= 0; --i) System.out.println(i); }`
	* 如果表达式只有一个参数，而且这个参数的类型可以通过推导得出，则小括号可以省略
* 函数式接口`@FunctionalInterface`
	* 只含有一个抽象方法的接口称为函数式接口
	* lambda表达式可以传递到函数接口
	* 重要的函数式接口：
		* `Predicate`
		* `Comparator`
* 方法引用：使用`::`操作符分隔方法名与对象或类名
	* `object::instanceMethod` 等价于`(a, b, ...) -> object.instanceMethod(a, b, ...)`
	* `Class::staticMethod` 等价于`(a, b, ...) -> Class.staticMethod(a, b, ...)`
	* `Class::instanceMethod` 等价于`(a, b, ...) -> a.instanceMethod(b, ...)`
	* `Class::new` 构造器引用等价于`(a, b, ...) -> new Class(a, b, ...)`
* 变量作用域：
	* 在lambda表达式中捕获的外部变量必须是最终变量(effective final)，外部变量在初始化以后就不会再赋新值。这是为了防止并发执行时的不安全
	* 在lambda表达式中使用`this`关键字时，是指创建这个lambda表达式的方法的`this`参数
	
	```
	public class Application() {
		public void init() {
			ActionListener listener = event -> {
				System.out.println(this.toString());
			}
		}
	}
	```
	表达式`this.toString()`会调用`Application`对象的`toString`方法，而不是`ActionListener`实例的方法
* `Comparator`接口：
	* Comparator接口包含很多方便的静态方法用于创建比较器，这些方法可以用于lambda表达式或者方法引用
	* 静态方法一般都有一个`KeyExtractor`接口参数，用于将类型`T`映射为一个可比较的类型。对要比较的对象应用这个函数，然后对返回的键完成比较
	* 重要API:
		* `Comparing()`
		* `ComparingInt/ComparingDouble/ComparingLong()`
		* `reversed()`

### 3. 内部类：语法复杂，使用较少，暂时放下 2018/09/30
### 4. 代理：与反射密切相关，使用较少，暂时放下 2018/09/30
