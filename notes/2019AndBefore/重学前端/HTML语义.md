# 前言

记录在《重学前端 - 04 | HTML语义：如何运用语义类标签来呈现Wiki网页？》使用到的标签，发现许多标签是自己一次都没使用过的，从MDN上摘录一遍。对于语义化引用winter的观点：

> “用对”语义标签 > “不用”语义标签（使用div, span代替） > “用错”语义标签
>
> 你可以尽量只用自己熟悉的语义标签，并且只在有把握的场景引入语义标签	。

# aside

aside 元素表示一个和其余页面内容几乎无关的部分，被认为是独立于该内容的一部分并且可以被单独的拆分出来而不会使整体受影响。其通常表现为侧边栏或者嵌入内容。

# article

article 元素表示文档、页面、应用或网站中的独立结构，其意在成为可独立分配的或可复用的结构，如在发布中，它可能是论坛帖子、杂志或新闻文章、博客、用户提交的评论、交互式组件，或者其他独立的内容项目。

# hgroup, h1, h2

The **HTML <hgroup> element** represents a multi-level heading for a section of a document. It groups a set of `<h1>–<h6>` elements.

```html
<hgroup>
    <h1>Calculus I</h1>
    <h2>Fundamentals</h2>
</hgroup>
```

# abbr

abbr 元素表示缩写，并可选择提供一个完整的描述(title)。

```html
<abbr title="World of Warcraft">WOW</abbr>
```

# hr

在页面中经常存在很长的横线，横线是不应该使用 hr 元素的。hr 元素表示段落级元素之间的主题转换（例如，一个故事中的场景的改变，或一个章节的主题的改变）。

# p

p 元素表示段落。p 元素是块级元素。

# strong

strong 元素表示文本十分重要，用粗体显示。

# blockquote, q, cite

blockquote 元素（或者 HTML 块级引用元素），代表其中的文字是引用内容。通常在渲染时，这部分的内容会有一定的缩进。若引文来源于网络，则可以将原内容的出处 URL 地址设置到 cite 特性上，若要以文本的形式告知读者引文的出处时，可以通过 cite 元素。

q 元素表示一个封闭的并且是短的行内引用的文本. 这个标签是用来引用短的文本，所以请不要引入换行符。

cite 元素表示一个作品的引用。它必须包含引用作品的符合简写格式的标题或者URL，它可能是一个根据添加引用元数据的约定的简写形式。

```html
<blockquote cite="https://www.huxley.net/bnw/four.html">
    <p>Words can be like X-rays, if you use them properly – they'll go through anything. You read and you're pierced.</p>
</blockquote>

<cite>– Aldous Huxley, Brave New World</cite>
```

# time

time 元素用来表示24小时制时间或者公历日期，若表示日期则也可包含时间和时区。

# figure, figcaption

figure代表一段独立的内容，经常与 figcaption 元素配合使用*,*并且作为一个独立的引用单元。当它属于主体(main flow)时，它的位置独立于主体。这个标签经常是在主文中引用的图片，插图，表格，代码段等等，当这部分转移到附录中或者其他页面时不会影响到主体。

figcaption 元素是与其相关联的图片的说明/标题，用于描述其父节点 figure 元素里的其他数据。

```html
<figure>
 <img src="https://.....440px-NeXTcube_first_webserver.JPG"/>
 <figcaption>The NeXT Computer used by Tim Berners-Lee at CERN.</figcaption>
</figure>
```

# dfn

dfn 元素表示术语的一个定义。

```html
<!-- Define "The Internet" -->
<p><dfn id="def-internet">The Internet</dfn> is a global system of interconnected networks that use the Internet Protocol Suite (TCP/IP) to serve billions of users worldwide.</p>
```

# nav, ol, ul

nav 元素表示描绘一个含有多个超链接的区域，这个区域包含转到其他页面，或者页面内部其他部分的链接列表。  

ol 有序列表。

ul 无序列表。

# pre, samp, code

pre 元素表示预定义格式文本。在该元素中的文本通常按照原文件中的编排，以等宽字体的形式展现出来，文本中的空白符（比如空格和换行符）都会显示出来。(紧跟在 pre 开始标签后的换行符也会被省略)。

samp 元素用于标识计算机程序输出。通常使用浏览器缺省的 monotype 字体。

code 元素呈现一段计算机代码。 默认情况下, 它以浏览器的默认等宽字体显示。

# 参考资料

+ [重学前端](https://time.geekbang.org/column/154)
+ [MDN文档](https://developer.mozilla.org/zh-CN/)
