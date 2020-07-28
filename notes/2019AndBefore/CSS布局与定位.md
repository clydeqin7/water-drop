# CSS布局与定位

### Q:块级(block)元素高度由什么决定？

**A:由内部文档流元素的高度总和决定。** **文档流**是指文档内元素的流动方向。



### Q:内联(inline)元素高度由什么决定？

**A:佛曰：不可测**。

> 参考阅读：[深入理解 CSS：字体度量、line-height 和 vertical-align](https://zhuanlan.zhihu.com/p/25808995)。



### Q:浮动时让子元素完全包含在父元素中

**A**: 在CSS中添加下列代码：

```
.clearfix::after {
  content: "";
  display: block;
  clear: both;
}
```

然后要浮动的子元素 的父级元素的```class```属性中添加"clearfix",如：

```
<p class="xxx clearfix">
	...
	浮动元素
	...
</p>
```

> 参考阅读：[浮动元素容器的clearing问题](http://www.ruanyifeng.com/blog/2009/04/float_clearing.html)



### Q:如何用CSS画出一个好看的形状，如三角形？

**A**:[The Shapes of CSS css-tricks](https://css-tricks.com/examples/ShapesOfCSS/),好多图形可以学习。



### Q:SVG设置距离上线边距一样

**A**:设置属性```vertical-align: top```