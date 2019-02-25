---
title: 在vue项目中使用axios的post请求遇到的问题
date: 2019-02-18 11:59:36
tags:
---
### 在使用axios这个ajax插件的时候，我们有些时候会遇到一些问题，比如：数据格式不正确

1、post请求需要传递form表单的数据给后台，而axios的post默认的contentType的数据格式是json，而我们要传的是form-data类型，以下有三种方案：

（1）使用js的序列化方法stringify（）

（2）使用formData函数，将form表单元素的name与value进行组合，实现表单数据的序列化（注：formData还有个功能：异步上传文件）

```bash
//通过FormData构造函数创建一个空对象
var formdata=new FormData();
//通过append()方法在末尾追加key为name值为laoliu的数据
formdata.append("name","laoliu");
```

（3）使用URLSearchParams处理axios发送的数据，但是要考虑它的兼容性，IE不支持
```bash
var params=new URLSearchParams()
params.append('name':'li')
```