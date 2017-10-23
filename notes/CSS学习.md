## CSS学习

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