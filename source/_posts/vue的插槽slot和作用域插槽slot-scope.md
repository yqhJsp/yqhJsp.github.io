---
title: vue的插槽slot和作用域插槽slot-scope
date: 2019-02-14 15:02:01
tags:
---

### 插槽slot的简单理解:

插槽，也就是slot，是组件中的一块HTML模板，这模块的显示与否由父组件决定。

### 单个插槽(默认插槽/匿名插槽)-顾名思义就是无name命名的slot

#### 在组件my-component中的形式如:
```bash
<div>
  <h2>我是子组件的标题</h2>
  <slot>
    只有在没有要分发的内容时才会显示。
  </slot>
</div>

```


#### 父组件模版:
```bash
<div>
  <h1>我是父组件的标题</h1>
  <my-component>
    <p>这是一些初始内容</p>
    <p>这是更多的初始内容</p>
  </my-component>
</div>

```
#### 渲染结果

```bash
<div>
  <h1>我是父组件的标题</h1>
  <div>
    <h2>我是子组件的标题</h2>
    <!--这里是slot-->
    <p>这是一些初始内容</p>
    <p>这是更多的初始内容</p>
    <!--slot--end-->
  </div>
</div>
```

### 具名插槽(可以用特性name进行命名,多个插槽的命名不能相同)

例子:有多个插槽slot的组件app-layout的模版

```bash
<div class="container">
  <header>
    <slot name="header"></slot>
  </header>
  <main>
    <slot></slot>
  </main>
  <footer>
    <slot name="footer"></slot>
  </footer>
</div>

```

父组件的模版:


```bash
<app-layout>
  <h1 slot="header">这里可能是一个页面标题</h1>

  <p>主要内容的一个段落。</p>
  <p>另一个主要段落。</p>

  <p slot="footer">这里有一些联系信息</p>
</app-layout>
```
渲染结果:
```bash
<div class="container">
  <header>
    <h1>这里可能是一个页面标题</h1>
  </header>
  <main>
    <p>主要内容的一个段落。</p>
    <p>另一个主要段落。</p>
  </main>
  <footer>
    <p>这里有一些联系信息</p>
  </footer>
 </div>
```

### 作用域插槽(可用作一个能被传递数据的可重用模版)

#### 在子组件中，只需将数据传递到插槽，就像你将 prop 传递给组件一样：
```bash
<ul>
  <slot name="item"
    v-for="item in items"
    :text="item.text">
    <!-- 这里写入备用内容 -->
  </slot>
</ul>
```

#### 在父级中，具有特殊特性 slot-scope 的元素必须存在，表示它是作用域插槽的模板。slot-scope 的值将被用作一个临时变量名，此变量接收从子组件传递过来的 prop 对象：

```bash
<my-awesome-list :items="items">
  <!-- 作用域插槽也可以是具名的 -->
  <li
    slot="item"
    slot-scope="{ text }"   //解构
    class="my-fancy-item">
    {{ text }}
  </li>
</my-awesome-list>
```



