# 脚本和模块

JavaScript 有 2 种源文件，一是脚本，二是模块（ES6引入的模块机制）。

脚本是可以由浏览器或者 node 环境引入执行的，而模块只能由 JavaScript 代码用 import 引入执行。

使用 script 标签引入模块，必须给 script 标签添加 `type="module"`。

```javascript
<script type="module" src="xxx.js"></script>
```

![脚本与模块的区别](https://i.loli.net/2019/05/09/5cd3ce4cd6bf0.png)

## import声明

import声明有 2 种用法：

+ 直接 import 一个模块（只能保证这个模块被执行，引用它的模块无法获得它的任何信息）
+ 带 from 的 import , 引入模块里的一些信息（引入模块的一部分信息，可以把它们变成本地变量）

```
import "mod" // 直接 import 一个模块
import v from "mod" // 把模块默认的导出值放入变量 v
```

带 from 的 import 细分又有三种用法：

+ `import x from "xxx.js"` 引入模块中导出的默认值
+ `import {a as x, modify} from "xxx.js"` 引入模块中的变量
+ `import * as x from "xxx.js"` 把模块中的所有变量以类似对象属性的方式引入

第一种方式还可以跟后两种组合使用

+ `import x，{a as x, modify} from "xxx.js"`
+ `import x，* as x from from "xxx.js"`

语法要求不带 as 的默认值永远在最前。**注意，这里的变量实际上仍受原来模块的控制**

### 模块a

```
export var a = 1;

export function modify(){
    a = 2;
}
```

### 模块b

```
import {a, modify} from "./a.js";

console.log(a);

modify();

console.log(a);
```

## export声明

与 import 相对，export 声明承担的是导出任务。

模块中导出变量的方式有两种

+ 独立使用 export 声明
+ 直接在声明型语句前添加 export 关键字

单独使用 export 声明，一个 export 关键字加上变量名列表：

```
export {a, b, c};
```

声明语句前添加 export 关键字，这里的 export 能添加在以下声明语句之前：

+ var
+ function（含 async 和 generator）
+ class
+ let
+ const

export 还可以跟 default 联合使用。`export default ` 表示导出一个默认变量值，它可以用于 function 和 class。这里导出的变量是没有名称的，可以使用 `import x from "./a.js"` 这样的语法，在模块中引入。

export default 还支持一种语法，后面跟一个表达式，如：

```
var a = {};
export default a;
```

**注意，这里导出的值，就是普通变量 a 的值，以后 a 的变化与导出的值就无关了，修改变量 a，不会使得其他模块中引入的 default 值发生改变**

在 import 语句前无法加入 export，但是我们可以直接使用 export from 语法。

```
export a from "a.js"
```

# 函数体



# 预处理

## var声明

## function声明

## class声明

# 指令序言机制

# 总结
