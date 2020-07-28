# CSS自学笔记	

```
设置字体可以列出几项供浏览器从前到后选择，字体单词不止一个的话需要用“”括起来
font-family:Helvetica, Arial, sans-serif;
```

- 字体默认大小值：16px

## Font 简写

许多字体的属性也可以通过 [`font`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font)的简写方式来设置 . 这些是按照以下顺序来写的：  [`font-style`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-style), [`font-variant`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-variant), [`font-weight`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-weight), [`font-stretch`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-stretch), [`font-size`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-size), [`line-height`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/line-height), and [`font-family`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-family).

在所有这些属性中，只有 `font-size` 和 `font-family` 是一定要指定的，如果你想要 `font`的简写形式。

一个正斜杠必须放在 [`font-size`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/font-size) 和 [`line-height`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/line-height) 属性之间。

一个完整的例子如下所示：

```
font: italic normal bold normal 3em/1.5 Helvetica, Arial, sans-serif;
```

### list-style 速记

上述提到的三种属性可以用一个单独的速记属性 [`list-style`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/list-style) 来设置。例如：

 

```
ul {
  list-style-type: square;
  list-style-image: url(example.png);
  list-style-position: inside;
}
```

可以被如下方式代替：

```
ul {
  list-style: square url(example.png) inside;
}
```

属性值可以任意顺序排列，你可以设置一个，两个或者三个值（该属性的默认值为 disc, none, outside），如果指定了 type 和 image，如果由于某种原因导致图像无法加载，则 type 将用作回退。

### start

`start` 属性允许你从1 以外的数字开始计数。例：

```
<ol start="3">
	<li>ddddsaf</li>
	<li>ddddsaf</li>
</ol>
```

### reversed

`reversed` 属性将启动列表倒计数。例：

``````
<ol start="3" reversed>
	<li>ddddsaf</li>
	<li>ddddsaf</li>
</ol>
``````

### value

`value` 属性允许设置列表项指定数值。例：

```
<ol>
	<li value="3">ddddsaf</li>
	<li value="6">ddddsaf</li>
</ol>
```

## 圆角边框

只需使用以下属性：

```
border-radius: 20px;
```

在不同的角落放置不同大小的边框半径, 您可以指定两个，三个或四个值, 就像您使用 [`padding`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/padding)and [`margin`](https://developer.mozilla.org/zh-CN/docs/Web/CSS/margin)一样:

```
/* 1st value is top left and bottom right corners,
   2nd value is top right and bottom left  */
border-radius: 20px 10px;
/* 1st value is top left corner, 2nd value is top right
   and bottom left, 3rd value is bottom right  */
border-radius: 20px 10px 50px;
/* top left, top right, bottom right, bottom left */
border-radius: 20px 10px 50px 0;
```

作为最后一点，您还可以创建椭圆形角（x半径与y半径不同）。两个不同的半径用正斜杠（/）分隔，您可以将其与值的任意组合组合。例如:

```
border-radius: 10px / 20px;
border-radius: 10px 30px / 20px 40px;
```
#### 文字水平居中

将一段文字置于容器的水平中点，只要设置text-align属性即可

```
text-align:center;
```

#### 容器的水平居中

先为该容器设置一个明确宽度，然后将[margin](https://developer.mozilla.org/zh-CN/docs/Web/CSS/margin)的水平值设为auto即可

```
p{
  width: 500px;
  margin: 0 auto;
}
```

#### 文字的垂直居中//TODO 还没试验出来

单行文字的垂直居中，只要将行高与容器高设为相等即可。

比如，容器中有一行数字。

```
<div id="container">1234567890</div>
```

然后CSS这样写：

```
div#container {height: 35px; line-height: 35px;}
```

如果有n行文字，那么将行高设为容器高度的n分之一即可。

#### 容器的垂直居中

比如，有一大一小两个容器，请问如何将小容器垂直居中？

```
<div id="big">
　　　　<div id="small">
　　　　</div>
</div>
```

首先，将大容器的定位为relative

[position介绍](https://developer.mozilla.org/zh-CN/docs/Web/CSS/position)

```
div#big{
　　　　position:relative;
　　　　height:480px;
}
```

然后，将小容器定位为absolute，再将它的左上角沿y轴下移50%，最后将它margin-top上移本身高度的50%即可。

```
div#small {
　　　　position: absolute;
　　　　top: 50%;
　　　　height: 240px;
　　　　margin-top: -120px;
　　}
```

使用同样的思路，也可以做出水平居中的效果。

#### CSS的优先级

如果同一个容器被多条CSS语句定义，那么哪一个定义[优先](http://www.vanseodesign.com/css/css-specificity-inheritance-cascaade/)呢？

基本规则是：

> 　　行内样式 > id样式 > class样式 > 标签名样式

比如，有一个元素：

> 　　<div id="ID" class="CLASS" style="color:black;"></div>

行内样式是最优先的，然后其他设置的优先性，从低到高依次为：

> 　　div < .class < div.class < #id < div#id < #id.class < div#id.class