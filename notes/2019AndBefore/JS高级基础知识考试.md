### Q1:

```
var object = {}
object.__proto__ ===  ????填空1????  // 为 true

var fn = function(){}
fn.__proto__ === ????填空2????  // 为 true
fn.__proto__.__proto__ === ????填空3???? // 为 true

var array = function(){}
array.__proto__ === ????填空4???? // 为 true
array.__proto__.__proto__ === ????填空5???? // 为 true

Function.__proto__ === ????填空6???? // 为 true
Array.__proto__ === ????填空7???? // 为 true
Object.__proto__ === ????填空8???? // 为 true

true.__proto__ === ????填空9???? // 为 true

Function.prototype.__proto__ === ????填空10???? // 为 true
```

### A:

```
空1：Object.prototype

空2：Function.prototype
空3：Object.prototype

空4：Function.prototype
空5：Object.prototype

*空6：Function.prototype
*空7：Function.prototype
*空8：Function.prototype

*空9：Boolean.prototype

空10：Object.prototype
```

### Q2:

```
function fn(){
    console.log(this)
}
new fn()

```

new fn() 会执行 fn，并打印出 this，请问这个 this 有哪些属性？这个 this 的原型有哪些属性？

### A:

```
this的自有属性为空，
this的原型有：constructor、--proto--, hasOwnProperty、isPrototypeOf、toString、valueOf等属性
```

### Q3：

>JSON 和 JavaScript 是什么关系？JSON 和 JavaScript 的区别有哪些？

### A:

```
  答1：抄袭与被抄袭的关系，JSON、JavaScript都是一门语言，JSON是抄袭JavaScript编写成的一门语言
  答2: 1. JSON没有抄袭 function 和 undefined
       2. JSON的名称必须是字符串，JSON字符串首尾必须是 "
       3. JSON没有原型链，JSON没有变量
```

### Q4:

>前端 MVC 是什么？
>请用代码大概说明 MVC 三个对象分别有哪些重要属性和方法。

### A:

```
答1：Model封装数据操作，
	View视图渲染，
	Controller控制器主要负责逻辑，1.Controller监听Model变化，Model一变，Controller就会去更新View；		2.Controller监听用户交互，用户点了提交或修改按钮，Controller就要去更新Model
答2：Model重要方法有初始化，获取数据，保存数据
	Controller重要属性有model,view, 方法有初始化model, 加载数据，绑定事件
	View重要方法是提供与HTML中的元素绑定的方法,可以通知controller用户进行了操作，也可以让contoller通知view更新显示内容
```



### Q5:

> 在 ES5 中如何用函数模拟一个类？

### A:

```
//狗类
function Dog(name, color) {
  //自有属性
  this.name = name
  this.color = color
}
//原型共有属性,所有实例共有的属性定义在prototype里，节约内存提升效率
Dog.prototype.eat = () => alert('啃骨头')
Dog.prototype.sleep = () => alert('睡觉')

//现在我实例生成了2个对象（2条狗），它们的自有属性是name, color;原型上有eat, sleep这2个属性
var dog1 = new Dog('大黄', 'yellow')
var dog2 = new Dog('小灰', 'gray')

dog1.name === dog2.name //false
dog1.eat === dog2.eat //true

```

### Q6:

> 用过 Promise 吗？举例说明。
>
> 如果要你创建一个返回 Promise 对象的函数，你会怎么写？举例说明

### A:

答1：

```
  用过，自己尝试过封装一个简单的AJAX，想让自己的AJAX函数拥有promise功能，就让AJAX函数返回一个Promise对象。
  AJAX = function(arg1, arg2){
    return new Promise((resolve, reject) => {
      //进行一些操作
      //监听变化
          -> 成功 调用resolve函数
          -> 失败 调用reject函数
    })
  }

  //使用的时候就可以使用链式操作
  AJAX(参数1, 参数2).then(成功， 失败)

```

答2：

```
function xxx(){
  return new Promise((f1, f2) => {
    doSomething()
    setTimeout(() => {
      //成功调用f1
      //失败调用f2
    }, 3000）
  })
}

xxx().then(success, fail)
//链式操作 success和success1可以一致
xxx().then(success, fail).then(success1, fail1)
```

### 参考答案

#### Q1

```
var object = {}
object.__proto__ ===  Object.prototype  // 为 true

var fn = function(){}
fn.__proto__ === Function.prototype  // 为 true
fn.__proto__.__proto__ === Object.prototype // 为 true

var array = function(){}
array.__proto__ === Array.prototype // 为 true [### 参考有误 ####]
array.__proto__.__proto__ === Object.prototype // 为 true

Function.__proto__ === Function.prototype // 为 true
Array.__proto__ === Function.prototype // 为 true
Object.__proto__ === Function.prototype // 为 true

true.__proto__ === Boolean.prototype // 为 true

Function.prototype.__proto__ === Object.prototype // 为 true
```

#### Q2

this 自身没有属性（只有一个隐藏的 `__proto__` 属性）
this 的原型是 fn.prototype，只有一个属性 constructor，且 constructor === fn（另外还有一个隐藏属性 `__proto__`，指向 Object.prototype）

#### Q3

1. 关系
   JSON是一种新的语言，但是是抄袭JS的
2. 区别
   JS有函数，JSON没有函数
   JS有变量，JSON没有变量
   JS有原型链，JSON没有原型链
   JS有undefined，JSON没有undefined
   JS属性名有时要加双引号，JSON属性名必须用双引号
   JS字符串可用单引号'string'或者双引号"string"，JSON字符串必须用双引号"string"

#### Q4

MVC 是什么
MVC 是一种设计模式（或者软件架构），把系统分为三层：Model数据、View视图和Controller控制器。
Model 数据管理，包括数据逻辑、数据请求、数据存储等功能。前端 Model 主要负责 AJAX 请求或者 LocalStorage 存储
View 负责用户界面，前端 View 主要负责 HTML 渲染。
Controller 负责处理 View 的事件，并更新 Model；也负责监听 Model 的变化，并更新 View，Controller 控制其他的所有流程。

代码说明

```
var model = {
    data: null,
    init(){}
    fetch(){}
    save(){}
    update(){}
    delete(){}
}
view = {
    init() {}
    template: '<h1>hi</h1'>
}
controller = {
    view: null,
    model: null,
    init(view, model){
        this.view = view
        this.model = model
        this.bindEvents()
    }
    render(){
        this.view.querySelector('name').innerText = this.model.data.name
    },
    bindEvents(){}
}
```

#### Q5

ES 5 没有 class 关键字，所以只能使用函数来模拟类。

```
function Human(name){
    this.name = name
}
Human.prototype.run = function(){}

var person = new Human('frank')

```

上面代码就是一个最简单的类，Human 构造函数创建出来的对象自身有 name 属性，其原型上面有一个 run 属性。

#### Q6

用过 Promise，比如 jQuery 或者 axios 的 AJAX 功能，都返回的是 Promise 对象。

```
$.ajax({url:'/xxx', method:'get'}).then(success1, error1).then(success2, error2)

```

如果我自己创建 Promise 对象，我会这么写

```
function asyncMethod(){
    return new Promise(function (resolve, reject){
        setTimeout(function(){
            成功则调用 resolve
            失败则调用 reject
        },3000)
    })
}
```