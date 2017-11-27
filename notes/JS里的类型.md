# JS里的类型

## 类型转换

### 任意类型转字符串

1. String(x)

   ![String(x)](https://i.loli.net/2017/11/27/5a1b65ade6bdc.png)

2. x.toString()

   ![x.toString()](https://i.loli.net/2017/11/27/5a1b65b485721.png)

3. x + ''

   ![x+''](https://i.loli.net/2017/11/27/5a1b65bbe5aed.png)

>对象采用大括号表示，这导致了一个问题：如果行首是一个大括号，它到底是表达式还是语句？
>
>```
>{ foo: 123 }
>
>```
>
>JavaScript引擎读到上面这行代码，会发现可能有两种含义。第一种可能是，这是一个表达式，表示一个包含`foo`属性的对象；第二种可能是，这是一个语句，表示一个代码区块，里面有一个标签`foo`，指向表达式`123`。
>
>为了避免这种歧义，JavaScript规定，如果行首是大括号，一律解释为语句（即代码块）。如果要解释为表达式（即对象），必须在大括号前加上圆括号。

### 任意类型转数字

1. Number(x)

   ![Number(x)](https://i.loli.net/2017/11/27/5a1b6b6560c16.png)

2. parseInt(x, 10) [MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/parseInt)

3. parseFloat(x) [MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/parseFloat)

4. x - 0

   ![](https://i.loli.net/2017/11/27/5a1b6b655049d.png)

5. +x

   ![+x](https://i.loli.net/2017/11/27/5a1b6b65581dc.png)

### 任意类型转布尔值

1. Boolean(x)

   ![Boolean(x)](https://i.loli.net/2017/11/27/5a1b6cec1f4c4.png)

2. !!x

>使用`Boolean`函数，可以将任意类型的变量转为布尔值。
>
>它的转换规则相对简单：除了以下六个值的转换结果为`false`，其他的值全部为`true`。
>
>- `undefined`
>- `null`
>- `-0`
>- `0`或`+0`
>- `NaN`
>- `''`（空字符串）

## 内存图

1. 你买一个 [8G 的内存条](https://item.jd.com/4071422.html)
2. 操作系统开机即占用 512MB
3. Chrome 打开即占用 1G 内存
4. Chrome 各每个网页分配一定数量的内存
5. 这些内存要分给页面渲染器、网络模块、浏览器外壳和 JS 引擎（V8引擎）
6. JS 引擎将内存分为代码区和数据区
7. 我们只研究数据区
8. 数据区分为 Stack（栈内存） 和 Heap（堆内存）
9. 简单类型的数据直接存在 Stack 里
10. 复杂类型的数据是把 Heap 地址存在 Stack 里

遇到问题就画图，不要分析。

### 面试题

```
​```javascript
var a = 1
var b = a
b = 2
请问 a 显示是几？  
​```

​```javascript
var a = {name: 'a'}
var b = a
b = {name: 'b'}
请问现在 a.name 是多少？
​```

​```javascript
var a = {name: 'a'}
var b = a
b.name = 'b'
请问现在 a.name 是多少？
​```

​```javascript
var a = {name: 'a'}
var b = a
b = null
请问现在 a 是什么？
​```
```

## 深复制

```
var a = 1
var b = a
b = 2 //这个时候改变 b
a 完全不受 b 的影响
那么我们就说这是一个深复制

```

对于简单类型的数据来说，赋值就是深拷贝。
对于复杂类型的数据（对象）来说，才要区分浅拷贝和深拷贝。

这是一个浅拷贝的例子

```
var a = {name: 'frank'}
var b = a
b.name = 'b'
a.name === 'b' // true

```

因为我们对 b 操作后，a 也变了

什么是深拷贝了，就是对 Heap 内存进行完全的拷贝。

```
var a = {name: 'frank'}
var b = deepClone(a) // deepClone 还不知道怎么实现
b.name = 'b'
a.name === 'a' // true
```

>参考资料：
>
>1. [JS 里的类型-写代码啦](https://xiedaimala.com/courses/ec3a5e28-02da-47d6-9226-927db23e82a2/tasks/61db0dcc-71d4-4f0c-822d-5f24ff0dd128)
>2. [JavaScript 标准参考教程-阮一峰](http://javascript.ruanyifeng.com/)
>
>

