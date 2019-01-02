# ES6的模块（Module）

# 前言

之前在项目中会用到`import`， `export` ， `require`等语法，一直不清楚它们的区别和来源，搜索了下看到阮一峰老师的文章[Module 的语法](http://es6.ruanyifeng.com/#docs/module)和其他的一些资料，了解了些常用概念，写篇笔记记录下。

# import和export

`import`和`export`都是ES6模块（Module）中的命令，通过`export`命令输出指定的代码，通过`import`命令输入。

## export命令

一个模块就是一个独立的文件。该文件内部的所有变量，外部无法获取。如果你希望外部能够读取模块内部的某个变量，就必须使用`export`关键字输出该变量。

### export的几种写法

```javascript
// profile.js
// 直接export
export var firstName = 'Michael';
var	lastName = 'Jackson';
var year = 1958;

// 使用大括号指定要输出的变量
export { lastName, year };	// 推荐写法，放在脚本尾部输出变量一目了然

```

#### `export`命令除了输出变量，还可以输出函数和类。

```javascript
export function sum (x, y) {
  return x + y;
};
```

#### `as`关键字重命名

通常情况下，`export`输出的变量就是本来的名字，但是可以使用`as`关键字重命名。

```javascript
function v1() { ... }
function v2() { ... }

export {
  v1 as streamV1,
  v2 as streamV2,
  v2 as streamLatestVersion
};
```

上面代码使用`as`关键字，重命名了函数`v1`和`v2`的对外接口。重命名后，`v2`可以用不同的名字输出两次。

### 其他要点

+ `export`语句输出的接口，与其对应的值是动态绑定关系，即通过该接口，可以取到模块内部实时的值。

```javascript
export var foo = 'bar';
setTimeout(() => foo = 'baz', 500);
```

上面代码输出变量`foo`，值为`bar`，500 毫秒之后变成`baz`。

+ `export`命令可以出现在模块的任何位置，只要处于模块顶层就可以。如果处于块级作用域内，就会报错。

```javascript
function foo() {
  export default 'bar' // SyntaxError
}
foo()
```

## import命令

使用`export`命令定义了模块的对外接口以后，其他 JS 文件就可以通过`import`命令加载这个模块。`import`命令会被 JavaScript 引擎静态分析，先于模块内的其他语句执行。

### import的几种写法

```javascript
// main.js
// 直接引入对应变量
import {firstName, lastName, year} from './profile.js';
// 使用as关键字重命名
import {lastName as surname} from './profile.js';
```

### 其他要点

+ `import`命令输入的变量都是只读的，因为它的本质是输入接口。

```javascript
import {a} from './xxx.js'

a = {}; // Syntax Error : 'a' is read-only;
a.foo = 'hello'; // 合法操作，但是很难查错，不建议使用
```

+ `import`命令具有提升效果，会提升到整个模块的头部，首先执行。
+ 由于`import`是静态执行，所以不能使用表达式和变量，这些只有在运行时才能得到结果的语法结构。

```javascript
// 报错
import { 'f' + 'oo' } from 'my_module';

// 报错
let module = 'my_module';
import { foo } from module;

// 报错
if (x === 1) {
  import { foo } from 'module1';
} else {
  import { foo } from 'module2';
}
```

+ 如果多次重复执行同一句`import`语句，那么只会执行一次，而不会执行多次。
+ `import`语句是 Singleton 模式。

```javascript
import { foo } from 'my_module';
import { bar } from 'my_module';

// 等同于
import { foo, bar } from 'my_module';
```

# 模块的整体加载

除了指定加载某个输出值，还可以使用整体加载，即用星号（`*`）指定一个对象，所有输出值都加载在这个对象上面。

```javascript
// circle.js

export function area(radius) {
  return Math.PI * radius * radius;
}

export function circumference(radius) {
  return 2 * Math.PI * radius;
}
```

逐一加载方法：

```javascript
// main.js

import { area, circumference } from './circle';

console.log('圆面积：' + area(4));
console.log('圆周长：' + circumference(14));
```

模块整体加载：

```javascript
import * as circle from './circle';

console.log('圆面积：' + circle.area(4));
console.log('圆周长：' + circle.circumference(14));
```

# export default命令

`export default`命令，为模块指定默认输出。

```javascript
// export-default.js
export default function () {
  console.log('foo');
}
```

其他模块加载该模块时，`import`命令可以为该匿名函数指定任意名字。

```javascript
// import-default.js
import customName from './export-default';
customName(); // 'foo'
```

本质上，**`export default`就是输出一个叫做`default`的变量或方法，然后系统允许你为它取任意名字**。

```javascript
// modules.js
function add(x, y) {
  return x * y;
}
export {add as default};
// 等同于
// export default add;

// app.js
import { default as foo } from 'modules';
// 等同于
// import foo from 'modules';
```

正是因为`export default`命令其实只是输出一个叫做`default`的变量，所以它后面不能跟变量声明语句。

```javascript
// 正确
export var a = 1;

// 正确
var a = 1;
export default a;

// 错误
export default var a = 1;
```

上面代码中，`export default a`的含义是将变量`a`的值赋给变量`default`。所以，最后一种写法会报错。

同样地，因为`export default`命令的本质是将后面的值，赋给`default`变量，所以可以直接将一个值写在`export default`之后。

```javascript
// 正确
export default 42;

// 报错
export 42;
```

上面代码中，后一句报错是因为没有指定对外的接口，而前一句指定对外接口为`default`。

`export default`也可以用来输出类。

```javascript
// MyClass.js
export default class { ... }

// main.js
import MyClass from 'MyClass';
let o = new MyClass();
```

# require和module.exports

`require`和`module.exports`都是[ComonJS规范](http://javascript.ruanyifeng.com/nodejs/module.html#toc5)中的内容，在ES6发布前，node模块中使用`require`引入模块，使用`module.exports`导出模块。

## module.exports

`module.exports`属性表示当前模块对外输出的接口，其他文件加载该模块，实际上就是读取`module.exports`变量。

```javascript
// a.js
module.exports = {
  a : function() {},
  b : 'xxx'
};
```

## require命令

使用`require`命令来加载模块文件。

```javascript
var example = require('./a.js'); // 引入a.js文件

console.log(example.b); // 'xxx'
```

# require和import不要混用

目前阶段，通过 Babel 转码，CommonJS 模块的`require`命令和 ES6 模块的`import`命令，可以写在同一个模块里面，但是最好不要这样做。因为`import`在静态解析阶段执行，所以它是一个模块之中最早执行的。下面的代码可能不会得到预期结果。

```javascript
require('core-js/modules/es6.symbol');
require('core-js/modules/es6.promise');
import React from 'React';
```

