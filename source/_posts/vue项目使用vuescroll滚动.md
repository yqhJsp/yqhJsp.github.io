---
title: vue项目使用vuescroll滚动
date: 2019-02-01 10:06:45
tags:
---
## 使用vue-scroll滚动条:

### （1）在vue项目下安装vuescroll组件:

   npm install vuescroll --save

### （2）局部引入:

import vueScroll from 'vuescroll'
import 'vuescroll/dist/vuescroll.css'

export default {
	components: {
		vueScroll
	},
	}

### html:

``` bash
<vue-scroll :ops="ops">
 你的内容
</vue-scroll>
```
	
###	配置:
```bash
ops: {
rail: {
	size: '10px'
},
bar: {
	onlyShowBarOnScroll: true,
	keepShow: false,
	background: '#c1c1c1',
	opacity: 0.5,
	hoverStyle: true,
	specifyBorderRadius: false,
	minSize: 0.3,
	size: '6px'
}
	}
-end
```
