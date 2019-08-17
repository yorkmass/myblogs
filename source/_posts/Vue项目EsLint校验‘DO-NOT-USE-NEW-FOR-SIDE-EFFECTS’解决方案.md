title: Vue项目EsLint校验‘DO NOT USE 'NEW' FOR SIDE EFFECTS’解决方案
author: Yaoyi
date: 2019-08-17 15:38:49
tags:
---
##### Vue项目EsLint校验‘DO NOT USE 'NEW' FOR SIDE EFFECTS’解决方案
***
我在写Vue项目时候在js里面写入如下代码报错
```
import Vue from 'vue'
import App from './App.vue'
 
new Vue({
  el: '#app',
  component: {
    App
  },
  template: '<App/>'
})
```
###### 解决方案：
1、定义一个变量xxx接受创建的Vue，然后在use里面添加xxx
```
import Vue from 'vue'
import App from './App.vue'
 
let myOwn = new Vue({
  el: '#app',
  component: {
    App
  },
  template: '<App/>'
})
Vue.use ({ xxx })
```
2、在new Vue上方添加一行注释，让Eslint不检查‘no-new’
```
import Vue from 'vue'
import App from './App.vue'
 
/* eslint-disable no-new */
new Vue({
  el: '#app',
  component: {
    App
  },
  template: '<App/>'
})
```