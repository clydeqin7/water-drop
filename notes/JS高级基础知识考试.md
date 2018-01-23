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

空6：Object.prototype
空7：Object.prototype
空8：Object.ptototype

空9：Object.prototype

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
this的自由属性为空，
this的原型有：constructor、--proto--, hasOwnProperty、isPrototypeOf、toString、valueOf等属性
```

### Q3：

>JSON 和 JavaScript 是什么关系？JSON 和 JavaScript 的区别有哪些？

### A:

```
答1：抄袭与被抄袭的关系，JSON、JavaScript都是一门语言，JSON是抄袭JavaScript编写成的一门语言
答2: 1. JSON没有抄袭 function 好 undefined
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
	View重要方法是提供与HTML中的元素绑定的方法
```



### Q5:

> 在 ES5 中如何用函数模拟一个类？

### A:

### Q6:

> 用过 Promise 吗？举例说明。
>
> 如果要你创建一个返回 Promise 对象的函数，你会怎么写？举例说明

### A:

答1：

```
用过，自己尝试过实现一个简单的AJAX，想让自己的AJAX函数拥有promise功能，就让AJAX函数返回一个Promise对象。
AJAX = function(){
  return new Promise((resolve, reject) => {
    //进行一些操作
    //监听变化
    	-> 成功 调用resolve函数
    	-> 失败 调用reject函数
  })
}

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

