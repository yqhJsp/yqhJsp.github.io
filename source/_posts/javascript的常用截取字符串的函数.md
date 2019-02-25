---
title: javascript的常用截取字符串的函数
date: 2019-02-01 15:59:48
tags:
---

### substr 、substring 、slice的用法

(1)substr获取从指定位置开始到指定字符数的字符;

(2)substring返回一个从指定开始的索引到结束的索引的字符串;

(3)slice：不改变原字符串，提取指定的字符串的一部分，返回一个新的字符串。

### 1、slice去除指定位置的字符串或新增

### 2、给"指针传递"的函数返回值加const,则返回值不能被直接修改,且该返回值只能被赋值给加const修饰的同类型指针   

(1)const用于修饰函数时，一般是const修饰类的成员函数（函数定义体），表示在函数体中成员变量不能改变；

其函数形式为：int ff(void)const;

(2)const修饰函数的返回值，用于返回常量；

如const int ff(); //返回的是常量,所以必须这么调用 const int a=ff();

(3)const int* i=0;  代表i是常量，里面的值不能够变

int* const i=;  代表指针i是常量，所指的内容可以修改

3、unshift倒叙排序
4、replace方法的语法是：stringObj.replace(rgExp, replaceText) 其中stringObj是字符串(string)，reExp可以是正则表达式对象(RegExp)也可以是字符串(string)，replaceText是替代查找到的字符串。。为了帮助大家更好的理解，下面举个简单例子说明一下

```bash
var s = "中文 - 标题".replace(/[\u4e00-\u9fa5]+\s+\-\s+/,''); 

console.log(s)
```