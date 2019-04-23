《21 | CSS选择器：伪元素是怎么回事儿？》（winter）的笔记

### 选择器的组合

在 CSS 规则中，选择器部分是一个选择器列表。

选择器列表实用逗号分隔的复杂选择器序列；复杂选择器则是用空格、大于号、波浪线等符号连接的复合选择器；符合选择器则是连写的简单选择器组合。

根据选择器列表的语法，选择器的连接方式可以理解为像四则运算一样有优先级。

+ 第一优先级
  - 无连接符号
+ 第二优先级
  - ”空格“
  - ”~“
  - ”+“
  - ”>"
  - "||"
+ 第三优先级
  - “,”

复杂选择器是针对节点关系的选择，它规定了五种连接符号。

+ **“空格”**：后代，表示选中所有符合条件的后代节点，例如 ”.a .b“ 表示选中所有 ”具有 class 为 a 的后代节点中 class 为 b 的节点“。
+ **“>”**：子代，表示选中符合条件的子节点，例如 ”.a>.b“ 表示：选中所有 ”具有 class 为 a 的子节点中，class 为 b 的节点“。
+ **“~”**：后继，表示选中所有符合条件的后继节点，后继节点即跟当前节点具有同一个父元素，并出现在它之后的节点，例如 ”.a~.b“ 表示选中所有具有 class 为 a 的后继种，class 为 b 的节点。
+ **”+“**：直接后继，表示选中符合条件的直接后继节点，直接后继节点即 nextSibling。例如 ”.a+.b“ 表示选中所有具有 class 为 a 的下一个 class 为 b 的节点。
+ **”||“**：列选择器，表示选中对应列中符合条件的单元格。

### 选择器的优先级

CSS 标准用一个三元组（a，b，c）来构成一个复杂选择器的优先级。

+ id 选择器的数目记为 a；
+ 伪类选择器和 class 选择器的数目记为 b;
+ 伪元素选择器和标签选择器数目记为 c;
+ ”*“ 不影响优先级。

CSS 标准建议用一个足够大的进制，获取 ”a-b-c“ 来表示选择器优先级。即：

```
spacificity = base * base * a + base * b + c
```

其中，base 是一个 ”足够大“ 的正整数。

**行内属性**的优先级**永远高于 CSS 规则**，浏览器提供了一个 ”口子“ ，就是在选择器前面加上 ”**!important**“。

这个用法非常危险，因为它相当于一个新的优先级，而且此优先级会高于行内属性。

同一优先级的选择器遵循 ”后面的覆盖前面的“ 原则。

实践中的建议：

+ 不要产生复杂的优先级计算，不要搞出过于复杂的选择器；
+ 根据 id 选单个元素，class 和 class 的组合选成组元素，tag 选择器确定页面风格；

### 伪元素

目前兼容性达到可用的微元素有以下几类：

+ ::first-line
+ ::first-letter
+ ::before
+ ::after

**::first-line 和 ::first-letter 是比较类似的伪元素**，其中一个表示元素的第一行，一个表示元素的第一个字母。下面的例子直观的展示出了效果：

```html
<p>this is an apple,<br/>
that is a pen</p>
```

```css
p::first-line{ color: red; }

p:first-letter{ text-transform: uppercase }
```

CSS 标准规定了 first-line 必须出现在最内层的块级元素之内。

```html
<div>
  <p id=a>First paragraph</p>
  <p>Second paragraph</p>
</div>
```

```css
div>p#a { color:green; }

div::first-line { color:blue; }
```

这段代码最终结果是第一行代码是蓝色，因为 p 是块级元素，所以微元素出现在块级元素之内，所以内层的 color 覆盖了外层的 color 属性。

如果把 p 换成 span，结果就是相反的。

```html
<div>
  <span id=a>First paragraph</span><br/>
  <span>Second paragraph</span>
</div>
```

```css
div>span#a { color:green; }

div::first-line { color:blue; }
```

这段代码最终结果是绿色，这说明伪元素在 span 之外。

::first-letter 的行为又有所不同，它的位置在所有标签之内。修改前面的代码测下吧。

CSS 标准只要求 ::first-line 和 ::first-letter 实现有限的几个 CSS 属性，都是文本相关的，相见下图。

![from winter 侵删](https://i.loli.net/2019/04/23/5cbe89fbe5dd8.png)



