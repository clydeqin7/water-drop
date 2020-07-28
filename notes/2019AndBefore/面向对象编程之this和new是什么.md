## 背诵的术语

手打一遍增强记忆！！！，MDN里可以找到以下内容

### Class 类

定义对象的特征。它是对象的属性和方法的模板定义。

### Object 对象

类的一个实例。

### Property 属性

对象的特征，比如颜色形状。

### Method 方法

对象的能力，比喻行走站立。

### Constructor 构造函数

对象初始化的瞬间，被调用的方法，通常它的名字与包含它的类一致。

### Inheritance 继承

一个类可以继承另一个类的特征。

### Encapsulation 封装

一种把数据和相关的方法绑定在一起使用的方法。

### Abstraction 抽象

结合复杂的继承，方法，属性的对象能够模拟现实的模型。

### Polymorphism 多态

多-意为‘许多’，态-意为‘形态’。不同类可以定义相同的方法或属性。



## this是什么？

this是Javascript语言的一个关键字。面试时常会考this的值是什么。

### 函数调用

JS里的三种函数调用形式：

```
func(arg1, arg2)
obj.child.method(arg1, arg2)
func.call(context, arg1, arg2)
```

函数调用其实只有一种形式：

```
func.call(context, arg1, arg2)
```

其他两种形式都可以等价的变成call的形式：

```
func(arg1, arg2) =>
func.call(undefined, arg1, arg2)

obj.child.method(arg1, arg2) =>
obj.child.method.call(obj, arg1, arg2)
```

**this**，就是call的context，就是「函数调用时call的第一个参数」

**浏览器有一条规则：**

>如果你传的 context 就 null 或者 undefined，那么 window 对象就是默认的 context（严格模式下默认 context 是 undefined）

那么

```
function f1(){
  console.log(this)
}

f1() 
```

f1()就将打印出window对象。

也可以自己指定this

```
f1.call(obj) // this就是obj对象了
```

**遇到关于this的值的问题，我们都将函数调用转成call的形式就很好解答了**

看一个例题

```
var color = 'green'
var test = {
  color:'blue',
  getColor: function(){
    var color = 'red'
    alert(this.color)
  }
}

var getColor = test.getColor
getColor() //
test.getColor() //


getColor() => getColor.call(undefined)
在结合上面浏览器的规则，我们可以知道此时的this是window对象,
var color = 'red'是一个全局变量,此时的color就是'green'

tset.getColor() => test.getColor.call(test)，此时的this就是test对象
可以明显的看到test对象的color属性是'blue'，此时的color就是'blue'

getColor() // green
test.getColor() // blue

```

## new是什么？

new是Javascript语言的一个关键字。

方方老师珠玉在前，在此借用下他的图片。

![](https://i.loli.net/2018/01/30/5a701dbb76f1d.png)

new关键字帮我们做了一下几件事

   	1. 帮我们创建临时对象
   	2. 给我们绑定原型
   	3. 给我们return临时对象
   	4. 给原型确定名字为prototype

new操作默认还加了个constructor属性

```
士兵.prototype = {
  constructor: 士兵
}
```

这个属性在我们重新对 士兵.prototype 赋值的时候就没了，可以有2种方式解决

```
1.赋值时使用 
士兵.prototype.xxx = ...

2.自己给constructor重新赋值
士兵.prototype = {
  constructor: 士兵,
  兵种:"美国大兵",
  行走:function(){ /*走俩步的代码*/},
  ...
}
```



>参考资料
>
>[JS 的 new 到底是干什么的？-方应杭](https://zhuanlan.zhihu.com/p/23987456?refer=study-fe)
>
>[this 的值到底是什么？一次说清楚-方应杭](https://zhuanlan.zhihu.com/p/23804247)
>
>[你怎么还没搞懂 this？-方应杭](https://zhuanlan.zhihu.com/p/25991271)
>
>[Javascript的this用法-阮一峰](http://www.ruanyifeng.com/blog/2010/04/using_this_keyword_in_javascript.html)

