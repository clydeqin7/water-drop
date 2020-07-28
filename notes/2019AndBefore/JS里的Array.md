# JS里的Array

## 基本用法

Array是JavaScript的内置对象，同时也是一个构造函数，可以用它生成新的数组。

window.Array 全局对象（也是函数）

```
Array(3) // {length:3} 
Array(3,3) // [3,3] 
new Array(3) 跟不加 new 一样的效果
new Array(3,3,) 跟不加 new 一样的效果
```

加不加 new 结果一样

window.Function 全局对象（也是函数），function是关键字

```
Function('x','y','return x+y')
new Function('x','y','return x+y')
```

**tips**: 简单类型+不+不一样，复杂类型+不+new一样。

## 函数声明方法总结

1. 具名函数

   ```
    function f(x,y){
        return x + y
    }

   ```

2. 匿名函数 + var

   ```
    var f
    f = function(x,y){ return x+y }

   ```

3. 具名函数 + var

   ```
    var f1 
    f1= function f2(x,y){
        return x+y
    }
    console.log(f2) // undefined

   ```

4. window.Function + var

   ```
    var f
    f = new Function('x','y','return x+y')
   ```

5.  **听课后新增：**箭头函数

   ```
   var f = (x, y) => {return x+y}
   var f = (x, y) => x+y //'{}'中只有一句话时可以同时去掉'{}','return'
   var f = n => n*n //只有一个参数可以省略'()' 
   ```

## JS 中数组的本质

人类理解：数组就是数据的有序集合
JS理解：数据就是原型链中有 Array.prototype 的对象

**重要式子：**```对象.__proto__ === 函数.prototype```

![方方老师手画图](https://i.loli.net/2017/12/08/5a2a4c97b6554.png)

## 伪数组

1. 有 0,1,2,3,4,5...n,length 这些 key 的对象
2. 原型链中没有 Array.prototype

这样的对象就是伪数组

目前知道的伪数组有

1. arguments 对象
2. document.querySelectAll('div') 返回的对象
3. document.getElementsById('$') 返回的对象

## 数组的 API

> 详见[Array-MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array)，本文只是列举一些常用的。

#### Array.isArray()

该方法用于确定传递的值是否是一个 Array。

```
Array.isArray([1, 2, 3]); //true
Array.isArray({}); //false
```

#### Array.prototype.concat()

该方法用于合并两个或多个数组。此方法不会更改现有数组，而是返回一个新数组。

```
var a = [1, 2, 3]; //[1, 2, 3]
var b = ['a', 'b', 'c']; //["a", "b", "c"]
var c = a.concat(b); //[1, 2, 3, "a", "b", "c"]
```

#### Array.prototype.join()

该方法将数组（或一个伪数组）的所有元素连接到一个以参数为分隔符的字符串中返回,不会改变数组,如果不提供参数，默认用逗号分隔。	

```
var a = [1, 2, 3];
a.join(); //"1,2,3"
a.join('|'); //"1|2|3"
a.join(']'); //"1]2]3"
```

#### Array.prototype.sort()

该方法在适当的位置对数组的元素进行排序，并返回数组。默认排序顺序是根据字符串Unicode码点。一般我们使用自定义排序方式来使用。

```
var a = [54, 26, 37, 2, 9];
a.sort(function (x, y){
  return x - y;
}) //[2, 9, 26, 37, 54]
a.sort(function (x, y){
  return y -x;
}) //[54, 37, 26, 9, 2]
```

#### Array.prototype.map()

该方法创建一个新数组，其结果是该数组中的每个元素都调用一个提供的函数后返回的结果。

```
var a = [1, 2, 3, 4, 5];
a.map(function (n){
  return n + 1;
}) //[2, 3, 4, 5, 6]
```

#### Array.prototype.forEach()

该方法对数组的每个元素执行一次提供的函数。**forEach**一般不返回值，只用来操作数据。如果需要有返回值，一般使用**map**方法。

```
var a = [1, 2, 3, 4, 5];
a.forEach( n => console.log(n)); //此处使用了箭头函数声明方法
//1
//2
//3
//4
//5
```

#### Array.prototype.slice()

该方法用于提取原数组的一部分，返回一个新数组，原数组不变。

它的第一个参数为起始位置（从0开始），第二个参数为终止位置（但该位置的元素本身不包括在内）。如果省略第二个参数，则一直返回到原数组的最后一个成员。

```
// 格式
arr.slice(start_index, upto_index);

// 用法
var a = ['a', 'b', 'c'];

a.slice(0) // ["a", "b", "c"]
a.slice(1) // ["b", "c"]
a.slice(1, 2) // ["b"]
a.slice(2, 6) // ["c"]
a.slice() // ["a", "b", "c"]
```

如果`slice`方法的参数是负数，则表示倒数计算的位置。

```
a.slice(-2) //["b", "c"]
a.slice(-2, -1) //["b"]	
```

#### Array.from()

该方法从一个类似数组或可迭代对象中创建一个新的数组实例返回。

```
var obj = {0:'a', 1:'b', 'length':2} //"object"
var arr = Array.from(obj) //["a", "b"]

Array.isArray(obj) //false
Array.isArray(arr) //true

```

#### Array.prototype.filter()

该方法的参数是一个函数，所有数组成员依次执行该函数，返回结果为`true`的成员组成一个新数组返回。该方法不会改变原数组。

```
var arr = [1, 2, 3, 4, 5, 6, 7, 8, 9, 10]
arr.filter(n => n%2 === 0 ) //使用箭头函数声明
// [2, 4, 6, 8, 10]
```

#### Array.prototype.reduce()

该方法依次处理数组的每个成员，最终累计为一个值。

```
var arr = [1, 2, 3, 4, 5]
arr.reduce(function (sum, n){
  console.log('sum='+sum+' ,n='+n)
  sum = sum + n
  return sum
})
//sum=1 ,n=2
//sum=3 ,n=3
//sum=6 ,n=4
//sum=10 ,n=5
//15

reduce的第一个参数是函数，函数接收以下四个参数：
1.累积变量，默认为数组的第一个成员  //必须
2.当前变量，默认为数组的第二个成员  //必须
3.当前位置（从0开始）
4.原数组

```

reduce还可以接收第二个参数，制定sum的初值

```
arr.reduce(function (sum, n){
  sum = sum + n
  return sum
}, 10) 
//25
```

## 如何将伪数组转换成真数组

方法1：真数组 = Array.prototype.slice.call(伪数组, 0)
方法2：真数组 = Array.from(伪数组)

```
var obj = {0:'a', 1:'b', 2:'c', 'length':3}  // 'Object'
var arr1 = Array.prototype.slice.call(obj, 0)
var arr2 = Array.from(obj)

Array.isArray(arr1) //true
Array.isArray(arr2) //true
```



> 参考链接：
>
> 1. [JS 自带的 API 之 Array-写代码了](https://xiedaimala.com/courses/ec3a5e28-02da-47d6-9226-927db23e82a2/tasks/b20f8aea-b602-4e6d-a42d-3ae52539fe4d)
> 2. [JavaScript 标准参考教程-阮一峰](http://javascript.ruanyifeng.com/)

