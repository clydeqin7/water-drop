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

## var

[var-MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/var)

> **variable 语句**声明了一个变量，可选地将其初始化为一个值。
>
> 变量声明，无论发生在何处，都在执行任何代码之前进行处理。用`var`声明的变量的作用域是它当前的执行上下文，它可以是嵌套的函数，也可以是声明在任何函数外的变量。如果你重新声明一个 JavaScript 变量，它将不会丢失其值。
>
> 将赋值给未声明变量的值在执行赋值时将其隐式地创建为全局变量（它将成为全局对象的属性）。

1. 声明变量的作用域限制在其声明位置的上下文中，而非声明变量总是全局的。

```javascript
function f() {
  x = 1
  var y = 'hello'
}

f()

console.log(x)  // 1
console.log(y)  // ReferenceError: y is not defined
```

2. 声明变量在任何代码执行前创建，而非声明变量只有在执行赋值操作的时候才会被创建。

```javascript
console.log(x) // ReferenceError: x is not defined
```

```javascript
var x
console.log(x) // "undefined"或""（不同浏览器实现不同）
console.log('hello') // "hello"
```

3. 声明变量是它所在上下文环境的不可配置属性，非声明变量是可配置的（如非声明变量可以被删除）。

```
var a = 1
b = 2

delete this.a
delete this.b 

console.log(a) // 1
console.log(b) // ReferenceError: b is not defined
```

## let

[let-MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Statements/let)

`let` 语句声明一个块级作用域的本地变量，并且可选的将其初始化为一个值。

```
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

