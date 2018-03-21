# Vue组件通信

## 父子组件通信

在 Vue 中，父子组件的关系可以总结为 **prop 向下传递，事件向上传递**。父组件通过 **prop**给子组件下发数据，子组件通过**事件**给父组件发送消息。看看它们是怎么工作的。

![](https://i.loli.net/2018/03/21/5ab1b867809d4.png)



[父子组件通信示例-JS Bin](http://jsbin.com/dezanaqiyi/edit?html,js,output)

```html
  <div id="app">
    <div>{{xxx}}</div>
    <button @click='childShow = true'>打开儿子</button>
    <child v-show='childShow' @ggg='childShow = false' message='message from parent'></child>
  </div> 
```

```javascript
Vue.component('child', {
  props: ['message'],
  template: `
    <div> {{message}} 
      <button @click="$emit('ggg')">关闭儿子</button>
    </div>`,
})

var app = new Vue({
  el: '#app',
  data: {
    xxx: 'hello world',
    childShow: false,
  }
})
```

## 爷孙组件通信

爷孙组件无法直接通信，需要通过父组件进行传递，通过2对父子组件的通信来实现爷孙通信。

[爷孙组件通信示例-JS Bin](http://jsbin.com/yoxovotuwe/1/edit?html,js,output)

```html
  <div id="app">
    <div>{{xxx}}</div>
    <button @click='showSunzi = true'>打开孙子</button>
    <hr>
    <child  :message='showSunzi' @babahao='yyy'></child>
  </div> 
```

```javascript
Vue.component('child', {
  props: ['message'],
  template:`
    <div>我是儿子 {{message}}
      <hr>
      <sunzi v-show="message" @yeyehao="$emit('babahao')"></sunzi>
    </div>
   `
})

Vue.component('sunzi', {
  template:`
    <div>我是孙子
        <button @click="$emit('yeyehao')">发消息给爷爷</button>
    </div>
  `
})
var app = new Vue({
  el: '#app',
  data: {
    xxx: 'hello world',
    showSunzi: false,
  },
  methods: {
    yyy(){
      console.log(1)
    }
  }
})
```

## 非父子组件的通信

有时候，非父子关系的两个组件之间也需要通信。在简单的场景下，可以使用一个空的 Vue 实例作为事件总线：

```javascript
var bus = new Vue()

// 触发组件 A 中的事件
bus.$emit('id-selected', 1)

// 在组件 B 创建的钩子中监听事件
bus.$on('id-selected', function (id) {
  // ...
})
```

还可以将Vue实例放入Vue的原型链中:

[非父子组件通信-原型链-JS Bin](http://jsbin.com/wopobolucu/edit?html,js,console,output)

```javascript
var eventHub = new Vue()
Vue.prototype.$eventHub = eventHub

Vue.component('component-a', {
  template: `<button @click='notify'>发消息给组件b</button>`,
  methods:{
    notify(){
      this.$eventHub.$emit('xxx', 'hello b')
    }
  },
});
Vue.component('component-b', {
  template: `<div>我是组件b收到的消息是: <span ref='show'></span></div>`,
  created(){
    this.$eventHub.$on('xxx', data=>{
// 子组件引用     //https://cn.vuejs.org/v2/guide/components.html#%E5%AD%90%E7%BB%84%E4%BB%B6%E5%BC%95%E7%94%A8
      this.$refs.show.textContent = data
    })
  }
});
var app = new Vue({
  el: '#app'
});
```

```css
  <div id="app">
    <component-a></component-a>
    <hr>
    <component-b></component-b>
  </div>
```

