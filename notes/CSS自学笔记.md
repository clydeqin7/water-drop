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