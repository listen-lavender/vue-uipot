# cascade select

> A Vue.js project

## Installation

``` bash
npm install vue-cascade
```

## Use

main.js
``` javascript
import Vue from 'vue'
import App from './App'
import mockTest from './mockTest'
import VueResource from 'vue-resource'

Vue.use(VueResource)

new Vue({
  el: '#app',
  template: '<App/>',
  components: { App }
})
```

App.vue
``` javascript
<template>
  <div id="app">
    <div class="three fields">
      <cascade :config="config" v-model="choice" @change="change"></cascade>
    </div>
    <div v-for="(value, key) in choice">
      {{ key }} : {{ value }}
    </div>
    <div>
    </div>
  </div>
</template>

<script>
import Cascade from 'src/index'
export default {
  name: 'app',
  data () {
      return {
          config: {
              "url":"/api/cascade",
          },
          choice: {}
      }
  },
  components: {
    cascade: Cascade
  },
  methods: {
      change:function(key, val) {
          console.log(key, val);
      },
  }
}
</script>

<style>
</style>

```

mockTest.js
``` javascript
import Mock from 'mockjs'

Mock.mock('/api/cascade', {
"cascade": [
{
"label": "省份",
"name": "province",
"param": "",
"url": "/api/province"
},
{
"label": "城市",
"name": "city",
"param": null,
"url": "/api/city?province={param}"
},
{
"label": "县镇",
"name": "town",
"param": null,
"url": "/api/town?city={param}"
}
],
"desc": "",
"stat": 1
})

Mock.mock('/api/province', {
"desc": "",
"options": [
{
"text": "北京",
"value": 1
},
{
"text": "湖北",
"value": 2
},
{
"text": "湖南",
"value": 3
}
],
"stat": 1
})

Mock.mock('/api/city?province=1', {
"desc": "",
"options": [
{
"text": "朝阳",
"value": 11
},
{
"text": "东城",
"value": 12
},
{
"text": "西城",
"value": 13
}
],
"stat": 1
})

Mock.mock('/api/city?province=2', {
"desc": "",
"options": [
{
"text": "黄冈",
"value": 21
},
{
"text": "武汉",
"value": 22
},
{
"text": "麻城",
"value": 23
}
],
"stat": 1
})

Mock.mock('/api/city?province=3', {
"desc": "",
"options": [
{
"text": "浏阳",
"value": 31
},
{
"text": "长沙",
"value": 32
},
{
"text": "岳阳",
"value": 33
}
],
"stat": 1
})

Mock.mock('/api/town?city=11', {
"desc": "",
"options": [ ],
"stat": 1
})

Mock.mock('/api/town?city=12', {
"desc": "",
"options": [ ],
"stat": 1
})

Mock.mock('/api/town?city=13', {
"desc": "",
"options": [ ],
"stat": 1
})

Mock.mock('/api/town?city=21', {
"desc": "",
"options": [
{
"text": "杨柳镇",
"value": 211
},
{
"text": "温泉镇",
"value": 212
}
],
"stat": 1
})

Mock.mock('/api/town?city=22', {
"desc": "",
"options": [
{
"text": "青山区",
"value": 221
},
{
"text": "东西湖区",
"value": 222
},
{
"text": "汉口区",
"value": 223
},
{
"text": "汉阳区",
"value": 224
}
],
"stat": 1
})

Mock.mock('/api/town?city=23', {
"desc": "",
"options": [
{
"text": "上林县",
"value": 231
}
],
"stat": 1
})

Mock.mock('/api/town?city=31', {
"desc": "",
"options": [
{
"text": "一水",
"value": 321
},
{
"text": "二水",
"value": 322
},
{
"text": "三水",
"value": 323
}
],
"stat": 1
})

Mock.mock('/api/town?city=32', {
"desc": "",
"options": [
{
"text": "橘子洲区",
"value": 321
}
],
"stat": 1
})

Mock.mock('/api/town?city=33', {
"desc": "",
"options": [
{
"text": "青山区",
"value": 331
},
{
"text": "红山区",
"value": 332
}
],
"stat": 1
})

module.exports =  Mock
```