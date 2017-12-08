# JS里的Array

## 基本用法

`Array`是JavaScript的内置对象，同时也是一个构造函数，可以用它生成新的数组。

window.Array 全局对象（也是函数）

```
Array(3) // {length:3} 
Array(3,3) // [3,3] 
new Array(3) 跟不加 new 一样的效果
new Array(3,3,) 跟不加 new 一样的效果
```

加不加 new 结果一样

window.Function 全局对象（也是函数）

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



## JS 中数组的本质

人类理解：数组就是数据的有序集合
JS理解：数据就是原型链中有 Array.prototype 的对象

![方方老师手画图](https://i.loli.net/2017/12/08/5a2a4c97b6554.png)

## 伪数组

1. 有 0,1,2,3,4,5...n,length 这些 key 的对象
2. 原型链中没有 Array.prototype

这样的对象就是伪数组

目前知道的伪数组有

1. arguments 对象
2. document.querySelectAll('div') 返回的对象

## 数组的 API

> 详见[Array-MDN](https://developer.mozilla.org/zh-CN/docs/Web/JavaScript/Reference/Global_Objects/Array)

未完待续...



> 参考链接：
>
> 1. [JS 自带的 API 之 Array-写代码了](https://xiedaimala.com/courses/ec3a5e28-02da-47d6-9226-927db23e82a2/tasks/b20f8aea-b602-4e6d-a42d-3ae52539fe4d)
> 2. [JavaScript 标准参考教程-阮一峰](http://javascript.ruanyifeng.com/)

