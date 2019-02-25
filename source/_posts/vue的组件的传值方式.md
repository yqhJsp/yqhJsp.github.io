---
title: vue的组件的传值方式
date: 2019-02-01 15:59:48
tags:
---
### 1、子组件向父组件传值
(1)父组件通过props传值
```bash
<gdp-analy :params="params":rsEcoConstruct="permiseMixin.rsEcoConstruct" ref="gdpAnaly"></gdp-analy>
```

(2)子组件接收父组件的参数
```bash
export default {
name: 'fundTrade',
components: {},
props: {
	params: Object,
	rsEcoConstruct: {
			type: String,
			default: 'false'
		}
	}
}
```

### 2、直接获取父级的值$parent.xxxx（局限性比较大，因为必须保证父级有该值）

### 二、父组件的事件触发响应子组件的请求
(1)在子组件添加事件
```bash
pChangeType() {
this.params.countType = this.$parent.countType
this.getEch1()
this.getTable1()
	}
```

(2)在父组件的点击事件
```bash
changeData(){
(1)//直接用$parent.xxx
this.$refs.childrenOne.pChangeType()	
```
注意：用props传值,避免时间钩子问题，导致父组件还没渲染完，拿不到值
```bash
this.$nextTick(() => {
this.$refs.childrenOne.init()	
])
```


### 三、vue的兄弟组件件的通信
（1）eventBus(vue2.0s版本才有)

```bash
步骤1：新建一个eventBus的js
import Vue from 'vue';
export default new Vue();

在要使用eventBus的地方导入import Bus from '@/assets/js/eventBus'
```
```bash
步骤2：在要派发参数或事件的组件中用$emit绑定派发事件
html:<a class="font-blue" href="javascript:;" @click="goCheck(item,0)">查看</a>

js:
goCheck(item, index) {
Bus.$emit('business-model-check', { item, index })
},
```
```bash
步骤3：在兄弟组件中用$on监听是否有该事件
mounted() {
this.init()
Bus.$on('business-model-check', params => {
this.getDetail(params)
})
},
```

