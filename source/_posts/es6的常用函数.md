---
title: es6的常用函数
date: 2019-02-01 15:59:48
tags:
---
1、es6的数组实例的 entries()，是键值对的遍历
```bash
for (let [index, elem] of ['a', 'b'].entries()) {
  console.log(index, elem);
}
// 0 "a"
// 1 "b"
```
2、对象的解构

```bash
let {list,children}=data
list=data.list
children=list.children
```
(注意，data中必须包含同名的对象）

3、数组的浅拷贝
```bash
let d=[1,2,3]
let arr=[...data,5,6]
(...扩展符号）
```

4、数组的解构
```bash
let [a,b,c]=[1,2,3]
console.log(a,b,c)
打印:1,2,3
```