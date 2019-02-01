---
title: vue的混合注入mixins
date: 2019-02-01 14:32:09
tags:
---
### vue的混合注入mixins的相关理解和使用

1、mixins 选项接受一个混入对象的数组；

2、这些混入实例对象可以像正常的实例对象一样包含选项，他们将在 Vue.extend() 里最终选择使用相同的选项合并逻辑合并。

3、如果混入包含一个钩子而创建组件本身也有一个，那么这两个函数会同时被调用；

4、Mixin 钩子按照传入顺序依次调用，并在调用组件自身的钩子之前被调用

#### 实例

```bash
子组件中导入
import glMixin from '@/assets/js/global-mixin'

export default {
	mixins: [glMixin, pageMixin]
	}
```



