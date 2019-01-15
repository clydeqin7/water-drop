CSS - 元素水平/垂直居中

### 前言

在 CSS 中，元素的水平/垂直居中一直是程序员高频接触的东西，实现的方法也多种多样，这里将相关方法收集于此，自己再实现下代码加深记忆。

### 水平居中

需考虑要居中的元素是[ 行内元素](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Inline_elemente)（如：`span`，`i`）还是[块级元素](https://developer.mozilla.org/zh-CN/docs/Web/HTML/Block-level_elements)（如：`div`，`p`）。

#### 行内元素

在需要居中元素的父容器上写`text-align: center;`即可。

```html
<!-- HTML -->
<div class="parent">
  <span class="child">内容区</span>
</div>
```

```css
/* CSS */
.parent{
  text-align: center;
}
```

#### 块级元素

给需要居中的元素一个显式的宽度，再`margin-left: auto;`，`margin-right: auto;` 。

```html
<!-- HTML -->
<div class="parent">
  <div class="child">内容区</div>
</div>
```

```css
/* CSS */
.child{
  width: 100px;
  margin-left: auto;
  margin-right: auto;
}
```

### 垂直居中

当`.parent`的高度**没有固定**时，`.child`使用`padding: 10px 0;`就能实现居中，当`.parent`的高度**固定**时则需要使用以下方式进行居中，建议开发时`.parent`的高度能不固定就不固定。

先放通用代码，后面具体实现时就不再贴出来了。

```html
<!-- HTML -->
<div class="parent">
  <div class="child">内容区</div>
</div>
```

```css
/* CSS */
.parent{
  height: 200px;
  border: 1px solid red;
}
.parent{
  width: 50px;
  height: 50px;
  border: 1px solid blue;
}
```

#### 1. absolute + margin auto

```CSS
/* CSS */
.parent{
  position: relative;
}
.child{
  position: absolute;
  margin: auto;
  top: 0;
  right: 0;
  bottom: 0;
  left: 0;
}
```

#### 2. absolute + margin-top

使用`margin-top: -50%;`， 这里的`-50%`是指`.child`自身高度的一半。

```css
/* CSS */
.parent{
  position: relative;
}
.child{
  position: absolute;
  top: 50%;
  margin-top: -25px;
}
```

#### 3. absolute + transform

这个方法需要考虑`transform`的兼容性。

```css
/* CSS */
.parent{
  position: relative;
}
.child{
  position: absolute;
  top: 50%;
  // 在实际项目中我们常常使用 translate(-50%, -50%) 实现水平和垂直居中
  transform: translateY(-50%);
}
```

#### 4. table 

布局改为`table`实现就能实现垂直居中。

```html
<!-- HTML -->
<table class="parent">
  <tr>
     <td class="child">内容区</td>
  </tr>
</table>
```

#### 5. div 实现 table

```css
/* CSS */
.parent{
  display: table-cell;
  vertical-align:middle;
}
```

还有一种复杂版：

```html
<!-- HTML -->
<div class="parent">
  <div class="parent-inner">
    <div class="child">内容区</div>
  </div>
</div>
```

```css
/* CSS */
.parent{
  display: table;
}
.parent-inner{
  display: table-cell;
  vertical-align:middle;
}
```

#### 6. line-height

设置`line-height`属性实现垂直居中，不推荐在项目中使用（有其他这么些方法不用，非要用这个？）

```css
/* CSS */
.child{
  line-height: 200px; // 父容器的高度
}
```

#### 7. flex

强烈推荐[flex](http://www.ruanyifeng.com/blog/2015/07/flex-grammar.html)，如丝般顺滑的实现水平垂直居中。

```css
/* CSS */
.parent{
  display: flex;
  align-items: center; //交叉轴（cross axis）如何对齐
}
```

#### 8. grid

同 flex 一样也是一种布局方式。

```css
/* CSS */
.parent{
  display: grid;
}

.child{
  align-self:center; 
}
```

### 总结

关于水平居中写得很少，其实很多垂直居中里的方法将应用于 y 轴的操作应用于 x 轴就能实现水平居中，实际项目选择适合的方法就好。

**水平居中**：

行内元素：父容器`text-align: center`即可。

块级元素：给需要居中的元素一个显式的宽度，再`margin-left: auto;`，`margin-right: auto;` 。	

**垂直居中**:

父容器高度**不固定**，子元素设置相同的`padding-top`和`padding-bottom`值就可实现垂直居中。

父容器高度**固定**:

1. absolute + margin auto
2. absolute + margin-top
3. absolute + transform
4. table
5. div 实现 table
6. line-height
7. flex
8. grid

### 参考资料

>[七种方式实现垂直居中-饥人谷](https://jscode.me/t/topic/1936)
>
>[CSS【日常处理总结】- GitHub](https://github.com/frontend9/fe9-library/issues/204)
>
>[六种实现元素水平居中 - w3cplus](https://www.w3cplus.com/css/elements-horizontally-center-with-css.html)





