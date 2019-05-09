---
title: axios 请求后台——JavaScript
date: 2019-05-09 20:00:00
comments: true #是否可评论
categories: axios #分类
toc: true #是否显示文章目
tags:   #标签
	- axios
	- vue
---




vue 创建一个新的项目—— vue init webpack my-project
<!-- more -->


## 安装

```
npm install axios
```
## 配置
main.js 里面进行配置

```
import axios from 'axios'
Vue.prototype.$axios = axios
```
## 使用
组件内应用

```
  mounted () {
    this.text()
  },
  methods: {
    async text () {
      let a = await this.$axios({
        method: 'get',
        url: 'http://172.16.60.169:1310/onlineInCave?class=vehicle'
      })
      console.log('j', a)
    }
  }
```
method: 获取方法，get 或者是 post
url: 后台地址
a 即是获取后台得到的数据
