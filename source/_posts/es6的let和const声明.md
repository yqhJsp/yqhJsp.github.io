---
title: es6的let和const声明
date: 2019-03-06 13:51:20
tags:
---
#### let声明
1、let声明在所在的代码块内有效，也就是有块级作用域作用；

2、let声明的变量一定要在声明后才能调用，不然会报错；

3、暂时性死区，只要在块级作用域使用let声明，那么声明的该变量就绑定了该区域。就算全局有同名的变量，但是由于区域内使用了let 命令，则该局部变量绑定了这个块级作用域，所以在let声明前赋值给该变量会报错；

4、不允许重复声明，let不允许在同一个作用域重复声明同一个变量，否则会报错；

5、var声明会变量提升的，内部的声明同名的变量，在调用函数时会污染外部的全局变量；

#### const声明
1、const声明一个只读常量。一旦声明，常量的值就不能改变。
```bash
const a=10;
a=16;
//这时候会报错：TypeError: Assignment to constant variable.
```
2、const声明的变量不能改变值，说明一旦声明变量，就必须立即初始化。

3、const的作用于与let声明相同，只有在声明所在的块作用于内有效。
```bash
if(true){
  const max=5;
}
max // Uncaught ReferenceError: MAX is not defined
```
4、const命令声明的常量也是不提升，同样存在暂时性死区，只能在声明的位置后面使用。
```bash
if (true) {
  console.log(MAX); // ReferenceError
  const MAX = 5;
}
```
5、const声明的常量，也与let一样不可重复声明。
```bash
var message = "Hello!";
let age = 25;

// 以下两行都会报错
const message = "Goodbye!";
const age = 30;
```

####　注意的事项:
(1)我们常说let和const声明的变量不能改变值,其实这个说法并不是说变量的值不得改动,而是变量指向的那个内存地址所保存的数据不得改动.对于简单的数据(数值、字符串、布尔值)，值就保存在变量指向的那个内存地址，因此等同于常量。但是对于复合型的数据（主要是对象和数组），变量指向的内存地址，保存的只是个指向实际数据的指针，const只能保证这个指针是固定的（即总是指向另一个固定的地址），至于它的指向的数据结构是不是可变，就完全控制不住了。因此，将一个对象声明为常量必须非常小心。
```bash
const foo={};
//为foo添加一个属性，可以成功
foo.name='xiaohua';

//将foo指向另一个对象，就会报错
foo={};// TypeError: "foo" is read-only
```