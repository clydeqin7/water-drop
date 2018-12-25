**前言**

​	CSS选择器的优先级是开发中常用且重要的知识，本文主要内容节选自[优先级-MDN](https://developer.mozilla.org/zh-CN/docs/Web/CSS/Specificity)，自己摘录一遍加深印象。

>  	浏览器通过**优先级**来判断哪一些属性值与一个元素最为相关，从而在该元素上应用这些属性值。优先级是基于不同种类[选择器](#怎么覆盖!important)组成的匹配规则。

# 优先级如何计算？

> 优先级就是分配给指定的CSS声明的一个权重，它由 匹配的选择器中的 每一种选择器类型的 数值 决定。
>
> 而当优先级与多个CSS声明中任意一个声明的优先级相等的时候，CSS中最后的那个声明将会被应用到元素上。
>
> 当同一个元素有多个声明的时候，优先级才会有意义。因为每一个直接作用于元素的CSS规则总是会接管/覆盖（take over）该元素从祖先元素继承而来的规则。

# 选择器的类型

>  优先级	1. **类型选择器**（type selectors）（如：`h1`）和**伪元素**（pseudo-elements）（如：
> ​     低           `::before`）
>
> ​      |	2. **类选择器**（class selectors）（如：`.example`），**属性选择器**（attributes selectors）（如：
> ​      |           `[type="radio"]`），**伪类**（pseudo-classes）（如：`:hover`）
>
> ​     高       3. **ID选择器**（如：`#example`）

**通配选择符**（universal selector）(`*`), **关系选择符**（combinators） (`+`, `>`, `~`, '')  和 **否定伪类**（negation pseudo-class）(`:not()`) 对优先级没有影响。（但是，在** :not() 内部声明**的选择器是会影响优先级）。

给元素添加的**内联样式** (例如, `style="font-weight:bold"`) 总会覆盖外部样式表的任何样式 ，因此可看作是具有**最高**的优先级。

# 例外!important规则

当在一个样式声明中使用一个`!important` 规则时，此声明将**覆盖任何其他声明**。

使用 `!important` 是一个坏习惯，应该尽量避免，因为这破坏了样式表中的固有的级联规则 使得调试找bug变得更加困难了。**当两条相互冲突的带有 `!important` 规则的声明被应用到相同的元素上时，拥有更大优先级的声明将会被采用**。

## 一些经验法则：

+ **一定**要优化考虑使用样式规则的优先级来解决问题而不是 `!important`
+ **只有**在需要覆盖全站或外部 css（例如引用的 ExtJs 或者 YUI ）的特定页面中使用 `!important`
+ **永远不要**在全站范围的 css 上使用` !important`
+ **永远不要**在你的插件中使用 `!important`

## 取而代之，你可以：

- 更好地利用CSS级联属性

- 使用更具体的规则。在您选择的元素之前，增加一个或多个其他元素，使选择器变得更加具体，并获得更高的优先级。

  ```html
  <div id="test">
    <span>Text</span>
  </div>
  ```

  ```css
  div#test span { color: green }
  span { color: red }
  div span { color: blue }
  ```

  无论你css语句的顺序是什么样的，文本都会是绿色的(green)，因为这一条规则是最有针对性、优先级最高的。（同理，无论语句顺序怎样，蓝色(blue)的规则都会覆盖红色(red)的规则）

## 什么的情况下可以使用 !important

（A）

```
1. 你的网站上有一个设定了全站样式的CSS文件，
2. 同时你（或是你同事）写了一些很差的内联样式。
```

在这种情况下，你就可以在你全局的CSS文件中写一些`!important`的样式来覆盖掉那些直接写在元素上的行内样式。

（B）

```css
#someElement p { color: blue; } p.awesome { color: red; }
```

在外层有 `#someElement` 的情况下，你怎样能使 `awesome `的段落变成红色呢？这种情况下，如果不使用 `!important` ，第一条规则永远比第二条的优先级更高。

## 怎么覆盖!important

（A）

只需再添加一条 带`!important` 的CSS规则，要么给这个给选择器更高的优先级（添加一个标签，ID或类）；或是添加一样选择器，把它的位置放在原有声明的后面。

```css
table td    { height: 50px !important; }
.myTable td { height: 50px !important; }
#myTable td { height: 50px !important; }	
```

（B）

或者使用相同的选择器，但是置于已有的样式之后： 

```css
td { height: 50px !important; }
```

（C）

或干脆改写原来的规则，以避免使用 ! important 。

# 例外的:not伪类

`:not` 否定伪类在优先级计算中不会被看作是伪类。 事实上， 在计算选择器数量时还是会把其中的选择器当做**普通选择器**进行计数。

```css
div.outer p {
  color:orange;
}

div:not(.outer) p {
  color: blueviolet;
}
```

```html
<div class="outer">
  <p>This is in the outer div.</p>
  <div class="inner">
    <p>This text is in the inner div.</p>
  </div>
</div>
```

[例子-codepen](https://codepen.io/clydeqin7/pen/GPEqro?&editable=true)

# 基于形式的优先级（Form-based specificity）

优先级是基于选择器的形式进行计算的。在下面的例子中，尽管选择器*[id="foo"] 选择了一个ID，但是它还是作为一个**属性选择器**来计算自身的优先级。

```css
* #foo {
  color: green;
}
*[id="foo"] {
  color: purple;
}
```

```HTML
<p id="foo">I am a sample text.</p>
```

[例子-codepen](https://codepen.io/clydeqin7/pen/EGXyXr?&editable=true)

虽然匹配了相同的元素，但是 **ID 选择器**拥有更高的优先级。所以第一条样式声明生效。

# 无视DOM树中的距离

```css
body h1 {
  color: green;
}
html h1 {
  color: purple;
}
```

```html
<html>
<body>
  <h1>Here is a title!</h1>
</body>
</html>
```

页面文字将渲染为紫色(purple)。

# 直接给目标元素添加样式和目标元素继承样式对比

为目标元素直接添加样式，永远比继承样式的优先级高，无视优先级的遗传规则。

```css
#parent {
  color: green;
}
h1 {
  color: purple;
}
```

```html
<html>
<body id="parent">
  <h1>Here is a title!</h1>
</body>
</html>
```

页面文字将渲染为紫色（purple），因为 `h1` 选择器明确的定位到了元素，但绿色选择器的仅仅继承自其父级。
