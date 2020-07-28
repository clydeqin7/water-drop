# var-let-const

## 变量提升

> 由于变量声明（以及其他声明[如函数声明]）总是在任意代码执行之前处理的，所以在代码中的任意位置声明变量总是等效于在代码开头声明。这意味着变量可以在声明之前使用，这个行为叫做“hoisting”。“hoisting”就像是把所有的变量声明移动到函数或者全局代码的开头位置。

```
console.log(a) // 1
a = 1
var a 

// 等价于

var a 
a = 1
console.log(a) // 1
```

## 作用域

ES6之前作用域总共只有两种——全局和局部（函数），ES6新增了一个块级作用域。

通过`var`声明的变量**没有**块级作用域。

使用 `let`和`const`声明的变量是**有**块级作用域。

## 暂时死区

所谓暂时死区，就是不能在初始化之前，使用变量。

## var

[var-MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/var)

> **variable 语句**声明了一个变量，可选地将其初始化为一个值。
>
> 变量声明，无论发生在何处，都在执行任何代码之前进行处理。用`var`声明的变量的作用域是它当前的执行上下文，它可以是嵌套的函数，也可以是声明在任何函数外的变量。如果你重新声明一个 JavaScript 变量，它将不会丢失其值。
>
> 将赋值给未声明变量的值在执行赋值时将其隐式地创建为全局变量（它将成为全局对象的属性）。

1.声明变量的作用域限制在其声明位置的上下文中，而非声明变量总是全局的。

```javascript
function f() {
  x = 1
  var y = 'hello'
}

f()

console.log(x)  // 1
console.log(y)  // ReferenceError: y is not defined
```

2.声明变量在任何代码执行前创建，而非声明变量只有在执行赋值操作的时候才会被创建。

```javascript
console.log(x) // ReferenceError: x is not defined
```

```javascript
var x
console.log(x) // "undefined"或""（不同浏览器实现不同）
console.log('hello') // "hello"
```

3.声明变量是它所在上下文环境的不可配置属性，非声明变量是可配置的（如非声明变量可以被删除）。

```javascript
var a = 1
b = 2

delete this.a
delete this.b 

console.log(a) // 1
console.log(b) // ReferenceError: b is not defined
```

## let

[let-MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/let)

[我用了两个月的时间才理解 let-方应杭](https://zhuanlan.zhihu.com/p/28140450)

>- let 声明的变量的作用域是块级的；
>- let 不能重复声明已存在的变量；
>- let 有暂时死区，不会被提升。

`let` 语句声明一个块级作用域的本地变量，并且可选的将其初始化为一个值。

1.**let**声明的变量只在其声明的块或子块中可用，这一点，与**var**相似。二者之间最主要的区别在于**var**声明的变量的作用域是整个封闭函数。

```javascript
function varTest() {
  var x = 1;
  if (true) {
    var x = 2;  // 同样的变量!
    console.log(x);  // 2
  }
  console.log(x);  // 2
}

function letTest() {
  let x = 1;
  if (true) {
    let x = 2;  // 不同的变量
    console.log(x);  // 2
  }
  console.log(x);  // 1
}
```

2.

```javascript
// for循环的小括号是一个作用域，而花括号又是一个作用域，而小括号的作用域是包裹住了大括号作用域
// for( let i = 0; i< 5; i++) { 循环体 } 在每次执行循环体之前，JS 引擎会把 i 在循环体的上下文中重新声明及初始化一次。
for(var i = 0; i < 5; i++){
  setTimeout(function(){
    console.log(i) //打印出5次 '5'
  }, 100) 
}

for(let i = 0; i < 5; i++){
  setTimeout(function(){
    console.log(i) //打印5次 '0','1','2','3','4'
  }, 100) 
}
```

## const

[const-MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/const)

> - 此声明创建一个常量，其作用域可以是全局或本地声明的块
> - 声明的时候，必须赋予初始值
> - 不能被重新赋值
> - 如果值是一个对象， 那么对象里面的属性是允许被修改的
> - 不能跟其他标识符重名

1.**const**是块级作用域,const的值不能通过重新赋值来改变，并且不能重新声明。

```javascript
const QAQ = 1
QAQ = 2 // TypeError: Assignment to constant variable.
const QAQ = 2 // SyntaxError: Identifier 'QAQ' has already been declared

```

2.如果值是一个对象， 那么对象里面的属性是允许被修改的

```
const V_V = {name: 'clyde', age: '35'}
console.log(V_V)  // {name: "clyde", age: "35"}
V_V.name = 'jack'
console.log(V_V) // {name: "jack", age: "35"}
```

## 图形记忆几种声明方式

![图来自方应杭](https://i.loli.net/2018/04/17/5ad56b3ebd277.png)