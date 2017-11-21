## JavaScript学习笔记1

> 本文主要引用：[JavaScript 标准参考教程-阮一峰](http://javascript.ruanyifeng.com/)

## 变量提升

JavaScript引擎的工作方式是，先解析代码，获取所有被声明的变量，然后再一行一行地运行。这造成的结果，就是所有的变量的声明语句，都会被提升到代码的头部，这就叫做变量提升（hoisting）。

```
console.log(a);
var a = 1;

```

上面代码首先使用`console.log`方法，在控制台（console）显示变量a的值。这时变量`a`还没有声明和赋值，所以这是一种错误的做法，但是实际上不会报错。因为存在变量提升，真正运行的是下面的代码。

```
var a;
console.log(a);
a = 1;

```

最后的结果是显示`undefined`，表示变量`a`已声明，但还未赋值。

请注意，变量提升只对`var`命令声明的变量有效，如果一个变量不是用`var`命令声明的，就不会发生变量提升。

```
console.log(b);
b = 1;
```

上面的语句将会报错，提示“ReferenceError: b is not defined”，即变量`b`未声明，这是因为`b`不是用`var`命令声明的，JavaScript引擎不会将其提升，而只是视为对顶层对象的`b`属性的赋值。

## 数据类型

JavaScript 语言的每一个值，都属于某一种数据类型。JavaScript 的数据类型，共有六种。（ES6 又新增了第七种 Symbol 类型的值，本教程不涉及。）

- 数值（number）：整数和小数（比如1和3.14）
- 字符串（string）：字符组成的文本（比如”Hello World”）
- 布尔值（boolean）：`true`（真）和`false`（假）两个特定值
- `undefined`：表示“未定义”或不存在，即由于目前没有定义，所以此处暂时没有任何值
- `null`：表示无值，即此处的值就是“无”的状态。
- 对象（object）：各种值组成的集合

通常，我们将数值、字符串、布尔值称为原始类型（primitive type）的值，即它们是最基本的数据类型，不能再细分了。而将对象称为合成类型（complex type）的值，因为一个对象往往是多个原始类型的值的合成，可以看作是一个存放各种值的容器。至于`undefined`和`null`，一般将它们看成两个特殊值。

对象又可以分成三个子类型。

- 狭义的对象（object）
- 数组（array）
- 函数（function）

狭义的对象和数组是两种不同的数据组合方式，而函数其实是处理数据的方法。JavaScript把函数当成一种数据类型，可以像其他类型的数据一样，进行赋值和传递，这为编程带来了很大的灵活性，体现了JavaScript作为“函数式语言”的本质。

这里需要明确的是，JavaScript的所有数据，都可以视为广义的对象。不仅数组和函数属于对象，就连原始类型的数据（数值、字符串、布尔值）也可以用对象方式调用。

## null 和 undefined

`null`与`undefined`都可以表示“没有”，含义非常相似。

`null`的特殊之处在于，JavaScript把它包含在对象类型（object）之中。

```
typeof null // "object"
```

## 布尔值

布尔值代表“真”和“假”两个状态。“真”用关键字`true`表示，“假”用关键字`false`表示。布尔值只有这两个值。

下列运算符会返回布尔值：

- 两元逻辑运算符： `&&` (And)，`||` (Or)
- 前置逻辑运算符： `!` (Not)
- 相等运算符：`===`，`!==`，`==`，`!=`
- 比较运算符：`>`，`>=`，`<`，`<=`

如果JavaScript预期某个位置应该是布尔值，会将该位置上现有的值自动转为布尔值。转换规则是除了下面六个值被转为`false`，其他值都视为`true`。

- `undefined`
- `null`
- `false`
- `0`
- `NaN`
- `""`或`''`（空字符串）

## for…in循环

`for...in`循环用来遍历一个对象的全部属性。

```
var obj = {
  x: 1,
  y: 2
};
var props = [];
var i = 0;

for (props[i++] in obj);

props // ["x", "y"]
```

`for...in`循环有两个使用注意点。

- 它遍历的是对象所有可遍历（enumerable）的属性，会跳过不可遍历的属性
- 它不仅遍历对象自身的属性，还遍历继承的属性

如果只想遍历对象本身的属性，可以使用`hasOwnProperty`方法，在循环内部判断一下是不是自身的属性。

```
for (var key in person) {
  if (person.hasOwnProperty(key)) {
    console.log(key);
  }
}
```

## with语句

`with`语句的格式如下：

```
with (object) {
  statements;
}
```

它的作用是操作同一个对象的多个属性时，提供一些书写的方便。

```
// 例一
with (o) {
  p1 = 1;
  p2 = 2;
}
// 等同于
o.p1 = 1;
o.p2 = 2;

// 例二
with (document.links[0]){
  console.log(href);
  console.log(title);
  console.log(style);
}
// 等同于
console.log(document.links[0].href);
console.log(document.links[0].title);
console.log(document.links[0].style);
```
## 数组

数组（array）是按次序排列的一组值。每个值的位置都有编号（从0开始），整个数组用方括号表示。

```
var arr = ['a', 'b', 'c'];
```

任何类型的数据，都可以放入数组。

```
var arr = [
  {a: 1},
  [1, 2, 3],
  function() {return true;}
];

arr[0] // Object {a: 1}
arr[1] // [1, 2, 3]
arr[2] // function (){return true;}
```

上面数组`arr`的3个成员依次是对象、数组、函数。

### 数组的本质

本质上，数组属于一种特殊的对象。

### length属性

数组的`length`属性，返回数组的成员数量。

```
['a', 'b', 'c'].length // 3

```

JavaScript使用一个32位整数，保存数组的元素个数。这意味着，数组成员最多只有4294967295个（232- 1）个，也就是说`length`属性的最大值就是4294967295。

只要是数组，就一定有`length`属性。该属性是一个动态的值，等于键名中的最大整数加上`1`。

```
var arr = ['a', 'b'];
arr.length // 2

arr[2] = 'c';
arr.length // 3

arr[9] = 'd';
arr.length // 10

arr[1000] = 'e';
arr.length // 1001

```

上面代码表示，数组的数字键不需要连续，`length`属性的值总是比最大的那个整数键大`1`。另外，这也表明数组是一种动态的数据结构，可以随时增减数组的成员。

`length`属性是可写的。如果人为设置一个小于当前成员个数的值，该数组的成员会自动减少到`length`设置的值。

```
var arr = [ 'a', 'b', 'c' ];
arr.length // 3

arr.length = 2;
arr // ["a", "b"]

```

上面代码表示，当数组的`length`属性设为2（即最大的整数键只能是1）那么整数键2（值为`c`）就已经不在数组中了，被自动删除了。

将数组清空的一个有效方法，就是将`length`属性设为0。

```
var arr = [ 'a', 'b', 'c' ];

arr.length = 0;
arr // []

```

如果人为设置`length`大于当前元素个数，则数组的成员数量会增加到这个值，新增的位置都是空位。

```
var a = ['a'];

a.length = 3;
a[1] // undefined

```

上面代码表示，当`length`属性设为大于数组个数时，读取新增的位置都会返回`undefined`。

如果人为设置`length`为不合法的值，JavaScript会报错。

```
// 设置负值
[].length = -1
// RangeError: Invalid array length

// 数组元素个数大于等于2的32次方
[].length = Math.pow(2, 32)
// RangeError: Invalid array length

// 设置字符串
[].length = 'abc'
// RangeError: Invalid array length

```

值得注意的是，由于数组本质上是对象的一种，所以我们可以为数组添加属性，但是这不影响`length`属性的值。

```
var a = [];

a['p'] = 'abc';
a.length // 0

a[2.1] = 'abc';
a.length // 0

```

上面代码将数组的键分别设为字符串和小数，结果都不影响`length`属性。因为，`length`属性的值就是等于最大的数字键加1，而这个数组没有整数键，所以`length`属性保持为0。

如果数组的键名是添加超出范围的数值，该键名会自动转为字符串。

```
var arr = [];
arr[-1] = 'a';
arr[Math.pow(2, 32)] = 'b';

arr.length // 0
arr[-1] // "a"
arr[4294967296] // "b"

```

上面代码中，我们为数组`arr`添加了两个不合法的数字键，结果`length`属性没有发生变化。这些数字键都变成了字符串键名。最后两行之所以会取到值，是因为取键值时，数字键名会默认转为字符串。

### 类似数组的对象

如果一个对象的所有键名都是正整数或零，并且有`length`属性，那么这个对象就很像数组，语法上称为“类似数组的对象”（array-like object）。

```
var obj = {
  0: 'a',
  1: 'b',
  2: 'c',
  length: 3
};

obj[0] // 'a'
obj[1] // 'b'
obj.length // 3
obj.push('d') // TypeError: obj.push is not a function

```

上面代码中，对象`obj`就是一个类似数组的对象。

但是，“类似数组的对象”并不是数组，因为它们不具备数组特有的方法。上面例子中，`obj`对象没有数组的`push`方法，使用该方法就会报错。

“类似数组的对象”的根本特征，就是具有`length`属性。只要有`length`属性，就可以认为这个对象类似于数组。但是有一个问题，这种`length`属性不是动态值，不会随着成员的变化而变化。

```
var obj = {
  length: 0
};
obj[3] = 'd';
obj.length // 0

```

上面代码为对象`obj`添加了一个数字键，但是`length`属性没变。这就说明了`obj`不是数组。

典型的“类似数组的对象”是函数的`arguments`对象，以及大多数 DOM 元素集，还有字符串。

```
// arguments对象
function args() { return arguments }
var arrayLike = args('a', 'b');

arrayLike[0] // 'a'
arrayLike.length // 2
arrayLike instanceof Array // false

// DOM元素集
var elts = document.getElementsByTagName('h3');
elts.length // 3
elts instanceof Array // false

// 字符串
'abc'[1] // 'b'
'abc'.length // 3
'abc' instanceof Array // false
```

数组的`slice`方法可以将“类似数组的对象”变成真正的数组。

```
var arr = Array.prototype.slice.call(arrayLike);
```

除了转为真正的数组，“类似数组的对象”还有一个办法可以使用数组的方法，就是通过`call()`把数组的方法放到对象上面。

```
function print(value, index) {
  console.log(index + ' : ' + value);
}

Array.prototype.forEach.call(arrayLike, print);

```

上面代码中，`arrayLike`代表一个类似数组的对象，本来是不可以使用数组的`forEach()`方法的，但是通过`call()`，可以把`forEach()`嫁接到`arrayLike`上面调用。

下面的例子就是通过这种方法，在`arguments`对象上面调用`forEach`方法。

```
// forEach 方法
function logArgs() {
  Array.prototype.forEach.call(arguments, function (elem, i) {
    console.log(i+'. '+elem);
  });
}

// 等同于 for 循环
function logArgs() {
  for (var i = 0; i < arguments.length; i++) {
    console.log(i + '. ' + arguments[i]);
  }
}

```

字符串也是类似数组的对象，所以也可以用`Array.prototype.forEach.call`遍历。

```
Array.prototype.forEach.call('abc', function (chr) {
  console.log(chr);
});
// a
// b
// c

```

注意，这种方法比直接使用数组原生的`forEach`要慢，所以最好还是先将“类似数组的对象”转为真正的数组，然后再直接调用数组的`forEach`方法。

```
var arr = Array.prototype.slice.call('abc');
arr.forEach(function (chr) {
  console.log(chr);
});
// a
// b
// c
```

### in 运算符

检查某个键名是否存在的运算符`in`，适用于对象，也适用于数组。

## 数组的空位

当数组的某个位置是空元素，即两个逗号之间没有任何值，我们称该数组存在空位（hole）。

```
var a = [1, , 1];
a.length // 3

```

上面代码表明，数组的空位不影响`length`属性。

需要注意的是，如果最后一个元素后面有逗号，并不会产生空位。也就是说，有没有这个逗号，结果都是一样的。

```
var a = [1, 2, 3,];

a.length // 3
a // [1, 2, 3]

```

上面代码中，数组最后一个成员后面有一个逗号，这不影响`length`属性的值，与没有这个逗号时效果一样。

数组的空位是可以读取的，返回`undefined`。

```
var a = [, , ,];
a[1] // undefined

```

使用`delete`命令删除一个数组成员，会形成空位，并且不会影响`length`属性。

```
var a = [1, 2, 3];
delete a[1];

a[1] // undefined
a.length // 3

```

上面代码用`delete`命令删除了数组的第二个元素，这个位置就形成了空位，但是对`length`属性没有影响。也就是说，`length`属性不过滤空位。所以，使用`length`属性进行数组遍历，一定要非常小心。

数组的某个位置是空位，与某个位置是`undefined`，是不一样的。如果是空位，使用数组的`forEach`方法、`for...in`结构、以及`Object.keys`方法进行遍历，空位都会被跳过。

```
var a = [, , ,];

a.forEach(function (x, i) {
  console.log(i + '. ' + x);
})
// 不产生任何输出

for (var i in a) {
  console.log(i);
}
// 不产生任何输出

Object.keys(a)
// []

```

如果某个位置是`undefined`，遍历的时候就不会被跳过。

```
var a = [undefined, undefined, undefined];

a.forEach(function (x, i) {
  console.log(i + '. ' + x);
});
// 0. undefined
// 1. undefined
// 2. undefined

for (var i in a) {
  console.log(i);
}
// 0
// 1
// 2

Object.keys(a)
// ['0', '1', '2']

```

这就是说，空位就是数组没有这个元素，所以不会被遍历到，而`undefined`则表示数组有这个元素，值是`undefined`，所以遍历不会跳过。