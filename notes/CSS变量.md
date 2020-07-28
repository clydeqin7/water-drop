# CSS变量

## 前言

今天看到一篇文章《妙用CSS变量，让你的CSS变得更心动》<sup>[1]</sup>，了解到「CSS变量」这个知识点，结合阮一峰老师的《CSS 变量教程》<sup>[2]</sup> 这篇文章，学习下「CSS变量」。

## CSS变量是什么？

**CSS变量**（**CSS variables**）又名**CSS自定义属性**（**CSS custom properties**），它定义的一个变量可以在文档中重复使用。

## CSS变量怎么使用？有啥注意事项？

### 基本用法

使用`--`开头声明一个变量，使用`var()`函数来使用这个变量。

```css
html{
	--foo: red;
	color: var(--foo);
}
```

### 最佳实践

定义在根伪类 `:root` 下，这样就可以在HTML文档的任何地方访问到它了：

```css
:root {
  --main-bg-color: brown;
}
```

### 作用域

同一个CSS变量，可以在多个选择器内声明。读取的时候，优先级最高的声明生效。这与CSS的"层叠"（cascade）规则是一致的。

变量的作用域就是它所在的选择器的有效范围。

### 注意事项

#### 变量名大小写敏感

​	`--foo`和`--Foo`就是两个不同变量名

#### `var()`函数可以接受第二个参数做默认值

```
var(--foo, #f2f2f2)
var(--foo, "Clyde")
var(--foo, 20px 10px) // 第二个参数不处理内部的逗号或空格，都视作参数的一部分
```

#### 变量值只能做属性值，不能做属性名

```
var(--foo): red; // 错误
color: var(--foo); // 正确
```

#### 变量值类型

+ **变量值为字符可与其他字符串拼接**

```
--bar: 'hello';
--foo: var(--bar)' world';
```

+ **变量值为数值，不能与数值单位直接连用，需要`calc()`函数**

```
.foo {
  --gap: 20;
  /* 无效 */
  margin-top: var(--gap)px;
  /* 有效 */
  margin-top: calc(var(--gap) * 1px);
}
```

+ **变量值带有单位，就不能写成字符串**

```
/* 无效 */
.foo {
  --foo: '20px';
  font-size: var(--foo);
}

/* 有效 */
.foo {
  --foo: 20px;
  font-size: var(--foo);
 }
```



## CSS变量能干啥，优势是啥？

变量这个概率在Less（`@foo`）和Sass（`$foo`）中早已存在，通过使用CSS变量（`--foo`）就能直接在CSS中使用，而不用引入前面提到的2种CSS预处理语言。

响应式布局里同一变量名设置不同值。

### JavaScript 操作

JavaScript 也可以检测浏览器是否支持 CSS 变量。

```javascript
const isSupported =
  window.CSS &&
  window.CSS.supports &&
  window.CSS.supports('--a', 0);

if (isSupported) {
  /* supported */
} else {
  /* not supported */
}
```

JavaScript 操作 CSS 变量的写法如下。

```javascript
// 设置变量
document.body.style.setProperty('--primary', '#7F583F');

// 读取变量
document.body.style.getPropertyValue('--primary').trim();
// '#7F583F'

// 删除变量
document.body.style.removeProperty('--primary');
```

这意味着，JavaScript 可以将任意值存入样式表。下面是一个监听事件的例子，事件信息被存入 CSS 变量。

```javascript
const docStyle = document.documentElement.style;

document.addEventListener('mousemove', (e) => {
  docStyle.setProperty('--mouse-x', e.clientX);
  docStyle.setProperty('--mouse-y', e.clientY);
});
```

那些对 CSS 无用的信息，也可以放入 CSS 变量。

```css
--foo: if(x > 5) this.width = 10;
```

上面代码中，`--foo`的值在 CSS 里面是无效语句，但是可以被 JavaScript 读取。这意味着，可以把样式设置写在 CSS 变量中，让 JavaScript 读取。

所以，CSS 变量提供了 JavaScript 与 CSS 通信的一种途径。

## CSS变量有啥实际应用？

TODO:

## 参考

[1] 妙用CSS变量，让你的CSS变得更心动：https://mp.weixin.qq.com/s/MvE8aolZtyvB7OOolHeL1w

[2] CSS 变量教程：http://www.ruanyifeng.com/blog/2017/05/css-variables.html

